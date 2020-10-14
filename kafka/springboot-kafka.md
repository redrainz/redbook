- ## 配置

```java
@EnableKafka
@Configuration
public class Config {

    @Bean
    public ConcurrentKafkaListenerContainerFactory<String, String> concurrentKafkaListenerContainerFactory() {
        ConcurrentKafkaListenerContainerFactory<String, String> factory = new ConcurrentKafkaListenerContainerFactory<>();
        Map<String, Object> props = new HashMap<>();
        props.put(ConsumerConfig.BOOTSTRAP_SERVERS_CONFIG, "192.168.200.43:9092,192.168.200.43:9093,192.168.200.43:9094");
        props.put(ConsumerConfig.GROUP_ID_CONFIG, "test");
        props.put(ConsumerConfig.ENABLE_AUTO_COMMIT_CONFIG, true);
        props.put(ConsumerConfig.AUTO_COMMIT_INTERVAL_MS_CONFIG, "100");
        props.put(ConsumerConfig.SESSION_TIMEOUT_MS_CONFIG, "15000");
        props.put(ConsumerConfig.KEY_DESERIALIZER_CLASS_CONFIG, StringDeserializer.class);
        props.put(ConsumerConfig.VALUE_DESERIALIZER_CLASS_CONFIG, StringDeserializer.class);
        factory.setConsumerFactory(new DefaultKafkaConsumerFactory<>(props));
        return factory;
    }

    @Bean
    public KafkaTemplate<String, String> kafkaTemplate() {
        Map<String, Object> producerProps = new HashMap<>();
        producerProps.put(ProducerConfig.BOOTSTRAP_SERVERS_CONFIG, "192.168.200.43:9092,192.168.200.43:9093,192.168.200.43:9094");
        producerProps.put(ProducerConfig.RETRIES_CONFIG, 0);
        producerProps.put(ProducerConfig.BATCH_SIZE_CONFIG, 16384);
        producerProps.put(ProducerConfig.LINGER_MS_CONFIG, 1);
        producerProps.put(ProducerConfig.BUFFER_MEMORY_CONFIG, 33554432);
        producerProps.put(ProducerConfig.KEY_SERIALIZER_CLASS_CONFIG, StringSerializer.class);
        producerProps.put(ProducerConfig.VALUE_SERIALIZER_CLASS_CONFIG, StringSerializer.class);
        return new KafkaTemplate<>(new DefaultKafkaProducerFactory<>(producerProps));

    }
}
```

- ## 生产者

```java
   @Autowired
    private KafkaTemplate<String, String> kafkaTemplate;

    public void start() {
        ListenableFuture<SendResult<String, String>> listenableFuture = kafkaTemplate.send("test", 0, "1key", "1data");
        ListenableFuture<SendResult<String, String>> listenableFuture1 = kafkaTemplate.send("test", 0, "0key", "0data");
        listenableFuture.addCallback(new ListenableFutureCallback<SendResult<String, String>>() {
            @Override
            public void onSuccess(SendResult<String, String> sendResult) {
                System.out.println("onSuccess: " + sendResult.getClass().getName() + "  " + sendResult);
            }

            @Override
            public void onFailure(Throwable throwable) {

                System.out.println("onFailure: " + throwable.getMessage());
            }
        });
        listenableFuture1.addCallback(new ListenableFutureCallback<SendResult<String, String>>() {
            @Override
            public void onSuccess(SendResult<String, String> sendResult) {
                System.out.println("onSuccess: " + sendResult.getClass().getName() + "  " + sendResult);
            }

            @Override
            public void onFailure(Throwable throwable) {

                System.out.println("onFailure: " + throwable.getMessage());
            }
        });

    }
```
- ## 消费者

```java
@Component
public class Listener {
    @KafkaListener(id = "test", topics = "test", containerFactory = "concurrentKafkaListenerContainerFactory")
    public void onMessage(ConsumerRecord<String, String> data) {
        System.out.println("onMessage:  " + data);
    }

    @KafkaListener(id = "test1", topics = "test", containerFactory = "concurrentKafkaListenerContainerFactory", idIsGroup = false, groupId = "test")
    public void onMessage2(ConsumerRecord<String, String> data) {
        System.out.println("onMessage2:  " + data);
    }

}
```

