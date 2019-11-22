## v2v data sync interface design

python 需要封装的接口
```c
client_t* create_client(enum client_type type, const char* major_version,
                        const char* minor_version, const char* host,
                        const char* username, const char* password,
                        const char* thumb_print);

int destroy_client(client_t* client);
int sync(client_t* src_client, client_t* dest_client, const char* src_volume,
         const char* dest_volume, uint64_t start[], uint64_t sector[],
         int length);
```

client_t 结构包含的内容
```c
typedef struct client {
  void* client;
  int (*read)(void* client, const char* volume_id, char* buf, uint64_t len,
              uint64_t offset);
  int (*write)(void* client, const char* volume_id, char* buf, uint64_t len,
               uint64_t offset);
  int (*close_client)(void* client);
} client_t;
```

## v2v client wrapper interface design
| informantion get | input | output |
| ---------------- | ------ | ------ |
| construct_vm | client vm object | standard vm object |
| construct_cluster | client cluster object | standard cluster object |
| construct_datacenter | client cluster datacenter | standard datacenter object |
| construct_host | client host object | standard host object |
| construct_vlan | client vlan object | standard vlan object |
| vlans | | standard vlans list |
| vms | | standard vm list |
| get_vm | vm_id | standard vm object | 
| get_vms | condition | standard vm list |
| datacenters | | standard datacenter list |
| get_datacenter | datacenter_id | standard datacenter object |
| clusters | standard cluster object | 
| get_cluster | cluster_id | standard cluster object |
| hosts | | standard host list |
| get_host | host_id | standard host object |
| query_cluster_vm_summary | | standard vm_summary |
| special for vmware |
| GetthumbPrint_esxi | 
| GetthumbPrint_vcenter |
| open_cbt |


| data operate | input | output |
| ------------ | ----- | ------ |
| construct_snapshot | client snapshot object | standard snapshot object |
| construct disk object | client snapshot object | standard snapshot object |
| snapshot_create | standard disk object | standard snapshot object |
| snapshot_delete | standard snapshot object | bool | 
| wait_task | | |
| query_snapshot_changes | two standard snapshot object | chnaged areas |
| create_volume | standard disk object | bool |
| delete_volume | standard disk object | bool |
| create_vm | standard vm object | bool |
| start_vm | standard vm object | bool |
| stop_vm | standard vm object | bool |
| special for elf and other |
| check boot disk | standard disk list | standard disk object |
| inject_drive | standard disk object | bool |