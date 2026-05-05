# Identify KafkaConsumer Configuration Issues
  Description
    Please indicate what is wrong with the following KafkaConsumer as written
    
    What issues will arise?
    What will the upstream/downstream impacts be?
    Especially if this topic receives 2000 messages per minute

# Python 3
    from kafka import KafkaConsumer

    def handle_message(msg):
        raise Exception(f"DATABASE IS DOWN!: {msg.id}")

    if __name__ == "main":
        consumer = KafkaConsumer(
            'my_topic',
            bootstrap_servers='localhost:9092',
            group_id='demo-group',
            auto_offset_reset='earliest',
            enable_auto_commit=False
        )

        consumer.subscribe()

        while True:
            msgs = consumer.poll()

            for msg in msgs:
                try:
                    handle_message(msg)
                except:
                    kafka.produce('dead-letter-queue', msg)
                finally:
                    consumer.commit()

