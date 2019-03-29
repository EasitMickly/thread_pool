# ���� RT-Thread ���̳߳�ʵ��

---

## 1�� ��������

### 1.1 �̳߳�

�̳߳���һ�ֶ��̴߳�����ʽ����������н�������ӵ����У�Ȼ���ڴ����̺߳��Զ�������Щ����

- �̳߳ع�������ThreadPoolManager�������ڴ����������̳߳أ�
- �����̣߳�WorkThread�����̳߳��е��̣߳�
- ����ӿڣ�Task����ÿ���������ʵ�ֵĽӿڣ��Թ������̵߳��������ִ�У�
- ������У�queue�������ڴ��û�д���������ṩһ�ֻ�����ơ�

### 1.2 �̳߳ص�����

������������У����������ٶ����Ǻܷ�ʱ��ģ���Ϊ����һ������Ҫ��ȡ�ڴ���Դ��������������Դ����Java�и�����ˣ����������ͼ����ÿһ�������Ա��ܹ��ڶ������ٺ�����������ա�������߷������Ч�ʵ�һ���ֶξ��Ǿ����ܼ��ٴ��������ٶ���Ĵ������ر���һЩ�ܺ���Դ�Ķ��󴴽������١�����������ж������������һ����Ҫ����Ĺؼ����⣬��ʵ�����һЩ"�ػ���Դ"����������ԭ���̳߳�Ҳ���ɴ˶�����

> ���̳߳ص�ʵ����Դ�� <https://github.com/armink/EasyDataManager> ��Դ��Ŀ

## 2�� Ӧ�ó���

ʹ���̳߳���Ϊ�˼�С�̱߳���Ŀ�����Ӧ��������������Ӱ�죬������ǰ�����̱߳����������ٵĿ������߳�ִ������Ŀ�������ǲ��ɺ��Եġ�����̱߳����������ٵĿ�����Ӧ�ó�������ܿ��Ժ��Բ��ƣ���ôʹ��/��ʹ���̳߳ضԳ�������ܲ�������̫���Ӱ�졣

- ��λʱ���ڴ��������Ƶ����������ʱ��϶̣�
- ��ʵʱ��Ҫ��ϸߡ�������յ�����֮���ٴ����̣߳������޷�����ʵʱ�Ե�Ҫ�󣬴�ʱ����ʹ���̳߳أ�
- ���뾭����Ը�ͻ�����¼������� Web �����������������ת������������������޴�������ʱʹ�ô�ͳ����������벻ͣ�Ĵ��������������̡߳���ʱ���ö�̬�̳߳ؿ��Ա�����������ķ�����

## 3���÷�

��Ҫͨ����������������ʹ���̳߳أ�

- �����̳߳�
- ��ʼ���̳߳�
- ��������̳߳�
- �����̳߳�
- ͬ����
- �ͷ�ͬ����

### 3.1 �����̳߳�

ͨ�� **thread_pool** �� **thread_pool_t** �����̳߳�

```c
//��ʽһ �ṹ������
thread_pool pool;

//��ʽ�� �ṹ��ָ������
thread_pool_t pool;
```
*ע�����Ĳ���**��ʽһ**�����̳߳�*

### 3.2 ��ʼ���̳߳�

- ԭ��

```c
init_thread_pool(thread_pool_t const pool, 
               uint8_t max_thread_num, 
               uint32_t thread_stack);
```

- API

|����|����|����|����|
|:---|:---|:---|:---|
|���|pool|thread_pool_t|����|
|���|max_thread_num|uint8_t|�߳�����|
|���|thread_stack|uint32_t|��ջ��С|
|����ֵ|error_code|thread_pool_err|����״̬|


- Demo

����һ���߳�����Ϊ5����ջ��СΪ1024 Byte���̳߳�

```c
thread_pool pool;

init_thread_pool(pool, "A", 5, 1024);	
```

### 3.3 �������

- ԭ��

```c
add_task(thread_pool_t const pool,
        void (*process)(void *arg), 
        void *arg);
```
- API 

|����|����|����|����|
|:---|:---|:---|:---|
|���|pool|thread_pool_t|����|
|���|process(void *arg)|void|��������|
|���|arg|void *|�����������|
|����ֵ|error_code|thread_pool_err|����״̬|


- Demo

�̳߳���������� task1������ʱ��ͨ����־���� task1 ���̳߳�A�е�����Ч����

```c
char str_a[]="A";
//��������
static void *task1(void *arg) {
    LOG_D("This is %s test ",(char*)arg);
	return NULL;
}
//�������
pool.addTask(&pool, task1, str_a);

```

### 3.4 �����̳߳�

- ԭ��

```c
destroy(thread_pool_t pool);
```

- API

|����|����|����|����|
|:---|:---|:---|:---|
|���|pool|thread_pool_t|����|
|����ֵ|error_code|thread_pool_err|����״̬|


- Demo

�����̳߳�

```c
pool.destroy(&pool);				
```
### 3.5 ͬ����

- ԭ��
```c
sync_lock(thread_pool_t pool)��
```
- API 

|���|����|����|����|
|:---|:---|:---|:---|
|���|pool|thread_pool_t|����|
|����ֵ|NULL|void*|����״̬|


- Demo

```c
pool.lock(&pool);	
```

### 3.6 �ͷ�ͬ����

- ԭ��

```c
sync_unlock(thread_pool_t pool)��
```

- API 

|���|����|����|����|
|:---|:---|:---|:---|
|���|pool|thread_pool_t|����|
|����ֵ|NULL|void*|����״̬|


- Demo

```c
pool.unlock(&pool);
```

## 4��ʾ��

����λ�� thread_pool_sample.c ��Դ��������£�

```c
#include <finsh.h>
#include "thread_pool.h"

static void task(void *arg) {
    LOG_I("The task on thread %.*s is running", RT_NAME_MAX, rt_thread_self()->name);
    rt_thread_delay(rt_tick_from_millisecond((uint32_t)arg));
    LOG_I("The task on thread %.*s will finish", RT_NAME_MAX, rt_thread_self()->name);
}

static void thread_pool_sample(uint8_t argc, char **argv) {
    thread_pool pool;

    init_thread_pool(&pool, "sam", 3, 1024);
    /* add 5 task to thread pool */
    pool.add_task(&pool, task, (void *)(rand() % 5000));
    pool.add_task(&pool, task, (void *)(rand() % 5000));
    pool.add_task(&pool, task, (void *)(rand() % 5000));
    pool.add_task(&pool, task, (void *)(rand() % 5000));
    pool.add_task(&pool, task, (void *)(rand() % 5000));
    /* wait 10S */
    rt_thread_delay(rt_tick_from_millisecond(10 * 1000));
    /* delete all task */
    pool.del_all(&pool);
    /* destroy the thread pool */
    pool.destroy(&pool);
}
MSH_CMD_EXPORT(thread_pool_sample, Run thread pool sample);
```

�������̴������£�

- thread_pool_sample �л��ʼ��һ�������� 3 ���̵߳��̳߳�
- ���̳߳���һ������� 5 ������
- ÿ������ִ��ʱ����ʱ 5S �����ֵ
- �ȴ� 10 S ɾ���߳���ʣ���ȫ������
- �����̳߳�

ʹ��ǰ���� menuconfig �п��� `THREAD_POOL_USING_SAMPLES` ѡ�

�������� Finsh/MSH ��ִ�� `thread_pool_sample` ������ɿ���ʾ������Ч�����������£�

```shell
msh />thread_pool_sample
[D/thread_pool] create thread success.Current total thread number is 1
[D/thread_pool] create thread success.Current total thread number is 2
[D/thread_pool] create thread success.Current total thread number is 3
[D/thread_pool] initialize thread pool success!
[D/thread_pool.sample] The task on thread sam_0 is running
[D/thread_pool] add a task to task queue success.
[D/thread_pool.sample] The task on thread sam_1 is running
[D/thread_pool] add a task to task queue success.
[D/thread_pool.sample] The task on thread sam_2 is running
[D/thread_pool] add a task to task queue success.
[D/thread_pool] add a task to task queue success.
[D/thread_pool] add a task to task queue success.
[D/thread_pool.sample] The task on thread sam_1 finish
[D/thread_pool.sample] The task on thread sam_1 is running
[D/thread_pool.sample] The task on thread sam_1 finish
[D/thread_pool.sample] The task on thread sam_1 is running
[D/thread_pool.sample] The task on thread sam_0 finish
[D/thread_pool.sample] The task on thread sam_2 finish
[D/thread_pool.sample] The task on thread sam_1 finish
[D/thread_pool] delete all wait task success
[D/thread_pool] Thread pool destroy success
```

## 5����ϵ��ʽ

* ά����[armink](https://github.com/armink)
* ��ҳ��https://github.com/armink-rtt-pkgs/thread_pool