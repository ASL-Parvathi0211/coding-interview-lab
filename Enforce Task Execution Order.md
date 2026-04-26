# Enforce Task Execution Order
  Description
    Please update the following airflow DAG so that get_orders will always execute before generate_order_processing_input.
    Additionally, add a dynamic task mapping to this DAG so each order can be processed in parallel dynamically.

# Python 3
from airflow import DAG
from datetime import datetime

dag = DAG(
    start_date=datetime(2023, 1, 1),
    schedule_interval='@daily',
    schedule_interval='@daily',
    dag_id="my_airflow_dag",
)

def get_orders_callable():
    return[1, 2, 3, 4]

def generate_task_input_data(orders):
    # need to invoke each task callable with { order_num: n }
    pass

get_orders = PythonOperator(
    task_id='get_orders',
    python_callable=get_orders_callable,
   dag=dag,
)

    # use result of get_orders to  compute the input for the dyanmic tasks
generate_order-processing_input = PythonOperator(
    task_id='generate_order_processing_input',
    python_callable=generate_task_input_data,
    dag = dag,
)

process_orders = PyhtonOperator.partial(
    task_id = "process_order",
    python_callable = process_order,
    dag = dag,
).expand_kwargs(genertae_order_processing_input.output)

    # a task definition

    # end task definition

    # implement dynamic task mapping to parallel process the orders


