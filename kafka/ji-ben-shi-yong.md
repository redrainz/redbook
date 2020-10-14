- ## 引用依赖

```xml
    <dependencies>
        <dependency>
            <groupId>org.apache.zookeeper</groupId>
            <artifactId>zookeeper</artifactId>
            <version>3.4.14</version>
        </dependency>
        <!-- https://mvnrepository.com/artifact/org.apache.kafka/kafka -->
        <dependency>
            <groupId>org.apache.kafka</groupId>
            <artifactId>kafka_2.12</artifactId>
            <version>2.2.0</version>
        </dependency>

```

- ## zookeeper

```java
        ZooKeeper zooKeeper = new ZooKeeper("192.168.200.43:2181,192.168.200.43:2182,192.168.200.43:2183",
                5000, event -> System.out.println("ZooKeeper: " + Json.encodeAsString(event)));

        //创建
        zooKeeper.create("/test", "test".getBytes(), ZooDefs.Ids.OPEN_ACL_UNSAFE, CreateMode.PERSISTENT,
                (int rc, String path, Object ctx, String name) ->
                        System.out.printf("rc:%d,path:%s,ctx:%s,name:%s\n", rc, path, ctx, name), "aa");
        TimeUnit.SECONDS.sleep(1);
        //存在
        Stat stat = zooKeeper.exists("/test", true);
        System.out.println("stat1: " + Json.encodeAsString(stat));
        TimeUnit.SECONDS.sleep(1);
        //修改数据
        stat = zooKeeper.setData("/test", UUID.randomUUID().toString().getBytes(), -1);
        System.out.println("stat2: " + Json.encodeAsString(stat));
        TimeUnit.SECONDS.sleep(1);
        System.out.println("data1: " + new String(zooKeeper.getData("/test", true, new Stat())));
        //添加子节点
        String node = zooKeeper.create("/test/test",
                UUID.randomUUID().toString().getBytes(),
                ZooDefs.Ids.OPEN_ACL_UNSAFE, CreateMode.PERSISTENT);
        System.out.println("child: " + Json.encodeAsString(node));
        TimeUnit.SECONDS.sleep(1);

        //zookeeper 链接状态
        System.out.println(Json.encodeAsString(zooKeeper.getState()));

        //删除子节点
        zooKeeper.delete("/test/test", -1);
        TimeUnit.SECONDS.sleep(1);

        //删除节点
        zooKeeper.delete("/test", -1);
        TimeUnit.SECONDS.sleep(1);

```
- ## 生产者

```java
        Map<String, Object> config = new HashMap<>();
        config.put(ProducerConfig.BOOTSTRAP_SERVERS_CONFIG, "192.168.200.43:9092,192.168.200.43:9093,192.168.200.43:9094");
        config.put(ProducerConfig.ACKS_CONFIG, "all");
        config.put(ProducerConfig.KEY_SERIALIZER_CLASS_CONFIG, "org.apache.kafka.common.serialization.StringSerializer");
        config.put(ProducerConfig.VALUE_SERIALIZER_CLASS_CONFIG, "org.apache.kafka.common.serialization.StringSerializer");
        KafkaProducer kafkaProducer = new KafkaProducer(config);
        kafkaProducer.send(new ProducerRecord("test1",1, "key", "value1"), (metadata, exception) -> {
            System.out.println("metadata: " + metadata.toString());
            System.out.println("exception: " + exception.toString());
        });
        kafkaProducer.close();
    }
```

- ## 消费者

```java
        Properties properties = new Properties();
        properties.setProperty(ConsumerConfig.BOOTSTRAP_SERVERS_CONFIG, "192.168.200.43:9092,192.168.200.43:9093,192.168.200.43:9094");
        properties.setProperty(ConsumerConfig.GROUP_ID_CONFIG, "test");
        properties.setProperty(ConsumerConfig.KEY_DESERIALIZER_CLASS_CONFIG, StringDeserializer.class.getName());
        properties.setProperty(ConsumerConfig.VALUE_DESERIALIZER_CLASS_CONFIG, StringDeserializer.class.getName());
        KafkaConsumer<String, String> kafkaConsumer = new KafkaConsumer<>(properties);
        kafkaConsumer.subscribe(Arrays.asList("test"));
        while (true) {
            ConsumerRecords<String, String> consumerRecords = kafkaConsumer.poll(Duration.ofMillis(1000));
            consumerRecords.forEach(consumerRecord -> System.out.println(consumerRecord.toString()));
            kafkaConsumer.commitSync();
        }
```