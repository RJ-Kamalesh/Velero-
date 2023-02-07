Would like to know the reason behind sudden failure of Velero backup in our Azure Kubernetes cluster.

Pasting the import gist of command output followed by,

kubectl logs deployment/velero -n velero
velero backup describe or kubectl get backup/ -n velero -o yaml
velero backup logs
k logs -n velero

Would like to know the reason behind sudden failure of Velero backup in our Azure Kubernetes cluster.

Pasting the import gist of command output followed by,

kubectl logs deployment/velero -n velero
velero backup describe or kubectl get backup/ -n velero -o yaml
velero backup logs
k logs -n velero

Environment:

Velero version (use velero version) : v1.9.5
Microsoft plugins of velero : v1.5.3[eastus_vto.txt](https://github.com/RJ-Kamalesh/Velero_Partially-Failed/files/10674316/eastus_vto.txt)

Kubernetes version : Server version v1.23.12 , Client version v1.23.4
Cloud Provider : Azure

�]0;root@UK-AZR-PUSREJ01: �root@UK-AZR-PUSREJ01:# velero get backup
NAME STATUS ERRORS WARNINGS CREATED EXPIRES STORAGE LOCATION SELECTOR
test PartiallyFailed 4 0 2023-01-27 06:14:07 +0000 UTC 18d default
test7feb Failed 0 0 2023-02-07 08:11:36 +0000 UTC 29d default
test7feb2 Failed 0 0 2023-02-07 08:15:49 +0000 UTC 29d default
velero-daily-20230203030035 PartiallyFailed 4 0 2023-02-03 03:00:35 +0000 UTC 25d default
velero-daily-20230202030034 PartiallyFailed 4 0 2023-02-02 03:00:34 +0000 UTC 24d default
velero-daily-20230201030034 PartiallyFailed 4 0 2023-02-01 03:00:34 +0000 UTC 23d default
velero-daily-20230131030033 PartiallyFailed 4 0 2023-01-31 03:00:33 +0000 UTC 22d default
velero-daily-20230130030032 PartiallyFailed 4 0 2023-01-30 03:00:32 +0000 UTC 21d default
velero-daily-20230129030031 PartiallyFailed 4 0 2023-01-29 03:00:31 +0000 UTC 20d default
velero-daily-20230128030030 PartiallyFailed 4 0 2023-01-28 03:00:30 +0000 UTC 19d default
velero-daily-20230127030044 PartiallyFailed 4 0 2023-01-27 03:00:44 +0000 UTC 18d default
velero-daily-20230126030043 PartiallyFailed 4 0 2023-01-26 03:00:43 +0000 UTC 17d default
velero-daily-20230125030042 PartiallyFailed 4 0 2023-01-25 03:00:42 +0000 UTC 16d default
velero-daily-20230124030041 PartiallyFailed 4 0 2023-01-24 03:00:41 +0000 UTC 15d default
velero-daily-20230123030040 PartiallyFailed 4 0 2023-01-23 03:00:40 +0000 UTC 14d default
velero-daily-20230122030026 PartiallyFailed 4 0 2023-01-22 03:00:26 +0000 UTC 13d default
velero-daily-20230121030025 PartiallyFailed 4 0 2023-01-21 03:00:25 +0000 UTC 12d default
velero-daily-20230120030024 PartiallyFailed 4 0 2023-01-20 03:00:24 +0000 UTC 11d default
velero-daily-20230119030023 PartiallyFailed 4 0 2023-01-19 03:00:23 +0000 UTC 10d default
velero-daily-20230118030022 PartiallyFailed 4 0 2023-01-18 03:00:22 +0000 UTC 9d default
velero-daily-20230117030021 PartiallyFailed 4 0 2023-01-17 03:00:21 +0000 UTC 8d default
velero-daily-20230116030020 PartiallyFailed 4 0 2023-01-16 03:00:20 +0000 UTC 7d default
velero-daily-20230115030019 PartiallyFailed 4 0 2023-01-15 03:00:19 +0000 UTC 6d default
velero-daily-20230114030018 PartiallyFailed 4 0 2023-01-14 03:00:18 +0000 UTC 5d default
velero-daily-20230113030017 PartiallyFailed 4 0 2023-01-13 03:00:17 +0000 UTC 4d default
velero-daily-20230112030016 PartiallyFailed 4 0 2023-01-12 03:00:16 +0000 UTC 3d default
velero-daily-20230111030015 PartiallyFailed 4 0 2023-01-11 03:00:15 +0000 UTC 2d default
velero-daily-20230110030014 PartiallyFailed 4 0 2023-01-10 03:00:14 +0000 UTC 1d default
velero-daily-20230109030013 PartiallyFailed 4 0 2023-01-09 03:00:13 +0000 UTC 17h default

time="2023-02-07T08:11:36Z" level=info msg="Getting backup item actions" backup=velero/test7feb logSource="pkg/controller/backup_controller.go:597"
time="2023-02-07T08:11:36Z" level=info msg="Setting up backup store to check for backup existence" backup=velero/test7feb logSource="pkg/controller/backup_controller.go:607"
time="2023-02-07T08:12:56Z" level=error msg="Error getting backup store for this location" backupLocation=default controller=backup-sync error="rpc error: code = Unknown desc = storage.AccountsClient#ListKeys: Failure responding to request: StatusCode=429 -- Original Error: autorest/azure: Service returned an error. Status=429 Code="TooManyRequests" Message="The request is being throttled as the limit has been reached for operation type - Read_ObservationWindow_00:05:00. For more information, see - https://aka.ms/srpthrottlinglimits\"" error.file="/go/src/velero-plugin-for-microsoft-azure/velero-plugin-for-microsoft-azure/object_store.go:217" error.function=main.getStorageAccountKey logSource="pkg/controller/backup_sync_controller.go:182"
time="2023-02-07T08:12:57Z" level=error msg="Error getting a backup store" backup-storage-location=velero/default controller=backup-storage-location error="rpc error: code = Unknown desc = storage.AccountsClient#ListKeys: Failure responding to request: StatusCode=429 -- Original Error: autorest/azure: Service returned an error. Status=429 Code="TooManyRequests" Message="The request is being throttled as the limit has been reached for operation type - Read_ObservationWindow_00:05:00. For more information, see - https://aka.ms/srpthrottlinglimits\"" error.file="/go/src/velero-plugin-for-microsoft-azure/velero-plugin-for-microsoft-azure/object_store.go:217" error.function=main.getStorageAccountKey logSource="pkg/controller/backup_storage_location_controller.go:127"
time="2023-02-07T08:12:57Z" level=info msg="BackupStorageLocation is invalid, marking as unavailable" backup-storage-location=velero/default controller=backup-storage-location logSource="pkg/controller/backup_storage_location_controller.go:110"
time="2023-02-07T08:12:57Z" level=error msg="Current BackupStorageLocations available/unavailable/unknown: 0/0/1, BackupStorageLocation "default" is unavailable: rpc error: code = Unknown desc = storage.AccountsClient#ListKeys: Failure responding to request: StatusCode=429 -- Original Error: autorest/azure: Service returned an error. Status=429 Code="TooManyRequests" Message="The request is being throttled as the limit has been reached for operation type - Read_ObservationWindow_00:05:00. For more information, see - https://aka.ms/srpthrottlinglimits\")" controller=backup-storage-location logSource="pkg/controller/backup_storage_location_controller.go:171"
time="2023-02-07T08:13:23Z" level=error msg="backup failed" controller=backup error="rpc error: code = Unknown desc = storage.AccountsClient#ListKeys: Failure responding to request: StatusCode=429 -- Original Error: autorest/azure: Service returned an error. Status=429 Code="TooManyRequests" Message="The request is being throttled as the limit has been reached for operation type - Read_ObservationWindow_00:05:00. For more information, see - https://aka.ms/srpthrottlinglimits\"" error.file="/go/src/velero-plugin-for-microsoft-azure/velero-plugin-for-microsoft-azure/object_store.go:217" error.function=main.getStorageAccountKey key=velero/test7feb logSource="pkg/controller/backup_controller.go:300"
time="2023-02-07T08:13:39Z" level=info msg="Validating BackupStorageLocation" backup-storage-location=velero/default controller=backup-storage-location logSource="pkg/controller/backup_storage_location_controller.go:131"
time="2023-02-07T08:13:39Z" level=info msg="BackupStorageLocations is valid, marking as available" backup-storage-location=velero/default controller=backup-storage-location logSource="pkg/controller/backup_storage_location_controller.go:116"
time="2023-02-07T08:13:39Z" level=error msg="Current BackupStorageLocations available/unavailable/unknown: 0/1/0)" controller=backup-storage-location logSource="pkg/controller/backup_storage_location_controller.go:173"
time="2023-02-07T08:13:39Z" level=info msg="Found 27 backups in the backup location that do not exist in the cluster and need to be synced" backupLocation=default controller=backup-sync logSource="pkg/controller/backup_sync_controller.go:211"
time="2023-02-07T08:13:39Z" level=info msg="Attempting to sync backup into cluster" backup=velero-daily-20230127030044 backupLocation=default controller=backup-sync logSource="pkg/controller/backup_sync_controller.go:219"
time="2023-02-07T08:13:39Z" level=info msg="Successfully synced backup into cluster" backup=velero-daily-20230127030044 backupLocation=default controller=backup-sync logSource="pkg/controller/backup_sync_controller.go:249"

�]0;root@UK-AZR-PUSREJ01: ~�root@UK-AZR-PUSREJ01
�]0;root@UK-AZR-PUSREJ01: �root@UK-AZR-PUSREJ01:# velero backup describe test7feb2
Name: �[1mtest7feb2�[0m
Namespace: velero
Labels: velero.io/storage-location=default
Annotations: velero.io/source-cluster-k8s-gitversion=v1.23.12
velero.io/source-cluster-k8s-major-version=1
velero.io/source-cluster-k8s-minor-version=23

Phase: �[31mFailed�[0m (run velero backup logs test7feb2 for more information)

Errors: 0
Warnings: 0

Namespaces:
Included: *
Excluded:

Resources:
Included: *
Excluded:
Cluster-scoped: auto

Label selector:

Storage Location: default

Velero-Native Snapshot PVs: auto

TTL: 720h0m0s

Hooks:

Backup Format Version:

Started: 2023-02-07 08:15:49 +0000 UTC
Completed: <n/a>

Expiration: 2023-03-09 08:15:49 +0000 UTC

Velero-Native Snapshots:
�]0;root@UK-AZR-PUSREJ01: �root@UK-AZR-PUSREJ01:#
�]0;root@UK-AZR-PUSREJ01: �root@UK-AZR-PUSREJ01:#
�]0;root@UK-AZR-PUSREJ01: �root@UK-AZR-PUSREJ01:#
�]0;root@UK-AZR-PUSREJ01: �root@UK-AZR-PUSREJ01:# k logs restic-2sskk -n velero
time="2023-02-07T08:10:42Z" level=info msg="Setting log-level to INFO"
time="2023-02-07T08:10:42Z" level=info msg="Starting Velero restic server v1.9.5 (2b5281f38aad2527f95b55644b20fb169a6702a7-dirty)" logSource="pkg/cmd/cli/restic/server.go:87"
1.675757442435557e+09 INFO controller-runtime.metrics Metrics server is starting to listen {"addr": ":8080"}
time="2023-02-07T08:10:42Z" level=info msg="Starting metric server for restic at address [:8085]" logSource="pkg/cmd/cli/restic/server.go:177"
time="2023-02-07T08:10:42Z" level=info msg="Starting controllers" logSource="pkg/cmd/cli/restic/server.go:188"
time="2023-02-07T08:10:42Z" level=info msg="Controllers starting..." logSource="pkg/cmd/cli/restic/server.go:219"
1.6757574425062695e+09 INFO Starting server {"path": "/metrics", "kind": "metrics", "addr": "[::]:8080"}
1.6757574425064323e+09 INFO Starting EventSource {"controller": "podvolumebackup", "controllerGroup": "velero.io", "controllerKind": "PodVolumeBackup", "source": "kind source: *v1.PodVolumeBackup"}
1.675757442506599e+09 INFO Starting Controller {"controller": "podvolumebackup", "controllerGroup": "velero.io", "controllerKind": "PodVolumeBackup"}
1.675757442506474e+09 INFO Starting EventSource {"controller": "podvolumerestore", "controllerGroup": "velero.io", "controllerKind": "PodVolumeRestore", "source": "kind source: *v1.PodVolumeRestore"}
1.675757442506642e+09 INFO Starting EventSource {"controller": "podvolumerestore", "controllerGroup": "velero.io", "controllerKind": "PodVolumeRestore", "source": "kind source: *v1.Pod"}
1.6757574425066628e+09 INFO Starting Controller {"controller": "podvolumerestore", "controllerGroup": "velero.io", "controllerKind": "PodVolumeRestore"}
1.6757574426075783e+09 INFO Starting workers {"controller": "podvolumebackup", "controllerGroup": "velero.io", "controllerKind": "PodVolumeBackup", "worker count": 1}
1.6757574426076603e+09 INFO Starting workers {"controller": "podvolumerestore", "controllerGroup": "velero.io", "controllerKind": "PodVolumeRestore", "worker count": 1}
�]0;root@UK-AZR-PUSREJ01: �root@UK-AZR-PUSREJ01:#
�]0;root@UK-AZR-PUSREJ01: �root@UK-AZR-PUSREJ01:#
�]0;root@UK-AZR-PUSREJ01: �root@UK-AZR-PUSREJ01:#
�]0;root@UK-AZR-PUSREJ01: �root@UK-AZR-PUSREJ01:#
�]0;root@UK-AZR-PUSREJ01: �root@UK-AZR-PUSREJ01:#
�]0;root@UK-AZR-PUSREJ01: �root@UK-AZR-PUSREJ01:# k logs restic-2sskk -n velero ��������������[C�[C�������������[12P�[12@restic-bfkjh
time="2023-02-07T08:10:38Z" level=info msg="Starting Velero restic server v1.9.5 (2b5281f38aad2527f95b55644b20fb169a6702a7-dirty)" logSource="pkg/cmd/cli/restic/server.go:87"
time="2023-02-07T08:10:38Z" level=info msg="Setting log-level to INFO"
1.675757438543832e+09 INFO controller-runtime.metrics Metrics server is starting to listen {"addr": ":8080"}
time="2023-02-07T08:10:38Z" level=info msg="Starting metric server for restic at address [:8085]" logSource="pkg/cmd/cli/restic/server.go:177"
time="2023-02-07T08:10:38Z" level=info msg="Starting controllers" logSource="pkg/cmd/cli/restic/server.go:188"
time="2023-02-07T08:10:38Z" level=info msg="Controllers starting..." logSource="pkg/cmd/cli/restic/server.go:219"
1.6757574386095107e+09 INFO Starting server {"path": "/metrics", "kind": "metrics", "addr": "[::]:8080"}
1.6757574386096985e+09 INFO Starting EventSource {"controller": "podvolumebackup", "controllerGroup": "velero.io", "controllerKind": "PodVolumeBackup", "source": "kind source: *v1.PodVolumeBackup"}
1.675757438609769e+09 INFO Starting Controller {"controller": "podvolumebackup", "controllerGroup": "velero.io", "controllerKind": "PodVolumeBackup"}
1.675757438609736e+09 INFO Starting EventSource {"controller": "podvolumerestore", "controllerGroup": "velero.io", "controllerKind": "PodVolumeRestore", "source": "kind source: *v1.PodVolumeRestore"}
1.6757574386098542e+09 INFO Starting EventSource {"controller": "podvolumerestore", "controllerGroup": "velero.io", "controllerKind": "PodVolumeRestore", "source": "kind source: *v1.Pod"}
1.6757574386098726e+09 INFO Starting Controller {"controller": "podvolumerestore", "controllerGroup": "velero.io", "controllerKind": "PodVolumeRestore"}
1.6757574387107615e+09 INFO Starting workers {"controller": "podvolumebackup", "controllerGroup": "velero.io", "controllerKind": "PodVolumeBackup", "worker count": 1}
1.6757574387107272e+09 INFO Starting workers {"controller": "podvolumerestore", "controllerGroup": "velero.io", "controllerKind": "PodVolumeRestore", "worker count": 1}
�]0;root@UK-AZR-PUSREJ01: �root@UK-AZR-PUSREJ01:#
�]0;root@UK-AZR-PUSREJ01: �root@UK-AZR-PUSREJ01:#
�]0;root@UK-AZR-PUSREJ01: �root@UK-AZR-PUSREJ01:#
�]0;root@UK-AZR-PUSREJ01: �root@UK-AZR-PUSREJ01:# k logs restic-bfkjh -n velero ������������������������[12P�[13@restic-x5v5f
time="2023-02-07T08:10:40Z" level=info msg="Starting Velero restic server v1.9.5 (2b5281f38aad2527f95b55644b20fb169a6702a7-dirty)" logSource="pkg/cmd/cli/restic/server.go:87"
time="2023-02-07T08:10:40Z" level=info msg="Setting log-level to INFO"
1.6757574406452508e+09 INFO controller-runtime.metrics Metrics server is starting to listen {"addr": ":8080"}
time="2023-02-07T08:10:40Z" level=info msg="Starting metric server for restic at address [:8085]" logSource="pkg/cmd/cli/restic/server.go:177"
time="2023-02-07T08:10:40Z" level=info msg="Starting controllers" logSource="pkg/cmd/cli/restic/server.go:188"
time="2023-02-07T08:10:40Z" level=info msg="Controllers starting..." logSource="pkg/cmd/cli/restic/server.go:219"
1.675757440743646e+09 INFO Starting server {"path": "/metrics", "kind": "metrics", "addr": "[::]:8080"}
1.675757440743859e+09 INFO Starting EventSource {"controller": "podvolumebackup", "controllerGroup": "velero.io", "controllerKind": "PodVolumeBackup", "source": "kind source: *v1.PodVolumeBackup"}
1.675757440743913e+09 INFO Starting Controller {"controller": "podvolumebackup", "controllerGroup": "velero.io", "controllerKind": "PodVolumeBackup"}
1.6757574407440953e+09 INFO Starting EventSource {"controller": "podvolumerestore", "controllerGroup": "velero.io", "controllerKind": "PodVolumeRestore", "source": "kind source: *v1.PodVolumeRestore"}
1.6757574407441623e+09 INFO Starting EventSource {"controller": "podvolumerestore", "controllerGroup": "velero.io", "controllerKind": "PodVolumeRestore", "source": "kind source: *v1.Pod"}
1.6757574407441702e+09 INFO Starting Controller {"controller": "podvolumerestore", "controllerGroup": "velero.io", "controllerKind": "PodVolumeRestore"}
1.6757574408453553e+09 INFO Starting workers {"controller": "podvolumebackup", "controllerGroup": "velero.io", "controllerKind": "PodVolumeBackup", "worker count": 1}
1.6757574408454797e+09 INFO Starting workers {"controller": "podvolumerestore", "controllerGroup": "velero.io", "controllerKind": "PodVolumeRestore", "worker count": 1}
�]0;root@UK-AZR-PUSREJ01: �root@UK-AZR-PUSREJ01:#:

Velero version (use velero version) : v1.9.5
Microsoft plugins of velero : v1.5.3
Kubernetes version : Server version v1.23.12 , Client version v1.23.4
Cloud Provider : Azure

�]0;root@UK-AZR-PUSREJ01: �root@UK-AZR-PUSREJ01:# velero get backup
NAME STATUS ERRORS WARNINGS CREATED EXPIRES STORAGE LOCATION SELECTOR
test PartiallyFailed 4 0 2023-01-27 06:14:07 +0000 UTC 18d default
test7feb Failed 0 0 2023-02-07 08:11:36 +0000 UTC 29d default
test7feb2 Failed 0 0 2023-02-07 08:15:49 +0000 UTC 29d default
velero-daily-20230203030035 PartiallyFailed 4 0 2023-02-03 03:00:35 +0000 UTC 25d default
velero-daily-20230202030034 PartiallyFailed 4 0 2023-02-02 03:00:34 +0000 UTC 24d default
velero-daily-20230201030034 PartiallyFailed 4 0 2023-02-01 03:00:34 +0000 UTC 23d default
velero-daily-20230131030033 PartiallyFailed 4 0 2023-01-31 03:00:33 +0000 UTC 22d default
velero-daily-20230130030032 PartiallyFailed 4 0 2023-01-30 03:00:32 +0000 UTC 21d default
velero-daily-20230129030031 PartiallyFailed 4 0 2023-01-29 03:00:31 +0000 UTC 20d default
velero-daily-20230128030030 PartiallyFailed 4 0 2023-01-28 03:00:30 +0000 UTC 19d default
velero-daily-20230127030044 PartiallyFailed 4 0 2023-01-27 03:00:44 +0000 UTC 18d default
velero-daily-20230126030043 PartiallyFailed 4 0 2023-01-26 03:00:43 +0000 UTC 17d default
velero-daily-20230125030042 PartiallyFailed 4 0 2023-01-25 03:00:42 +0000 UTC 16d default
velero-daily-20230124030041 PartiallyFailed 4 0 2023-01-24 03:00:41 +0000 UTC 15d default
velero-daily-20230123030040 PartiallyFailed 4 0 2023-01-23 03:00:40 +0000 UTC 14d default
velero-daily-20230122030026 PartiallyFailed 4 0 2023-01-22 03:00:26 +0000 UTC 13d default
velero-daily-20230121030025 PartiallyFailed 4 0 2023-01-21 03:00:25 +0000 UTC 12d default
velero-daily-20230120030024 PartiallyFailed 4 0 2023-01-20 03:00:24 +0000 UTC 11d default
velero-daily-20230119030023 PartiallyFailed 4 0 2023-01-19 03:00:23 +0000 UTC 10d default
velero-daily-20230118030022 PartiallyFailed 4 0 2023-01-18 03:00:22 +0000 UTC 9d default
velero-daily-20230117030021 PartiallyFailed 4 0 2023-01-17 03:00:21 +0000 UTC 8d default
velero-daily-20230116030020 PartiallyFailed 4 0 2023-01-16 03:00:20 +0000 UTC 7d default
velero-daily-20230115030019 PartiallyFailed 4 0 2023-01-15 03:00:19 +0000 UTC 6d default
velero-daily-20230114030018 PartiallyFailed 4 0 2023-01-14 03:00:18 +0000 UTC 5d default
velero-daily-20230113030017 PartiallyFailed 4 0 2023-01-13 03:00:17 +0000 UTC 4d default
velero-daily-20230112030016 PartiallyFailed 4 0 2023-01-12 03:00:16 +0000 UTC 3d default
velero-daily-20230111030015 PartiallyFailed 4 0 2023-01-11 03:00:15 +0000 UTC 2d default
velero-daily-20230110030014 PartiallyFailed 4 0 2023-01-10 03:00:14 +0000 UTC 1d default
velero-daily-20230109030013 PartiallyFailed 4 0 2023-01-09 03:00:13 +0000 UTC 17h default

time="2023-02-07T08:11:36Z" level=info msg="Getting backup item actions" backup=velero/test7feb logSource="pkg/controller/backup_controller.go:597"
time="2023-02-07T08:11:36Z" level=info msg="Setting up backup store to check for backup existence" backup=velero/test7feb logSource="pkg/controller/backup_controller.go:607"
time="2023-02-07T08:12:56Z" level=error msg="Error getting backup store for this location" backupLocation=default controller=backup-sync error="rpc error: code = Unknown desc = storage.AccountsClient#ListKeys: Failure responding to request: StatusCode=429 -- Original Error: autorest/azure: Service returned an error. Status=429 Code="TooManyRequests" Message="The request is being throttled as the limit has been reached for operation type - Read_ObservationWindow_00:05:00. For more information, see - https://aka.ms/srpthrottlinglimits\"" error.file="/go/src/velero-plugin-for-microsoft-azure/velero-plugin-for-microsoft-azure/object_store.go:217" error.function=main.getStorageAccountKey logSource="pkg/controller/backup_sync_controller.go:182"
time="2023-02-07T08:12:57Z" level=error msg="Error getting a backup store" backup-storage-location=velero/default controller=backup-storage-location error="rpc error: code = Unknown desc = storage.AccountsClient#ListKeys: Failure responding to request: StatusCode=429 -- Original Error: autorest/azure: Service returned an error. Status=429 Code="TooManyRequests" Message="The request is being throttled as the limit has been reached for operation type - Read_ObservationWindow_00:05:00. For more information, see - https://aka.ms/srpthrottlinglimits\"" error.file="/go/src/velero-plugin-for-microsoft-azure/velero-plugin-for-microsoft-azure/object_store.go:217" error.function=main.getStorageAccountKey logSource="pkg/controller/backup_storage_location_controller.go:127"
time="2023-02-07T08:12:57Z" level=info msg="BackupStorageLocation is invalid, marking as unavailable" backup-storage-location=velero/default controller=backup-storage-location logSource="pkg/controller/backup_storage_location_controller.go:110"
time="2023-02-07T08:12:57Z" level=error msg="Current BackupStorageLocations available/unavailable/unknown: 0/0/1, BackupStorageLocation "default" is unavailable: rpc error: code = Unknown desc = storage.AccountsClient#ListKeys: Failure responding to request: StatusCode=429 -- Original Error: autorest/azure: Service returned an error. Status=429 Code="TooManyRequests" Message="The request is being throttled as the limit has been reached for operation type - Read_ObservationWindow_00:05:00. For more information, see - https://aka.ms/srpthrottlinglimits\")" controller=backup-storage-location logSource="pkg/controller/backup_storage_location_controller.go:171"
time="2023-02-07T08:13:23Z" level=error msg="backup failed" controller=backup error="rpc error: code = Unknown desc = storage.AccountsClient#ListKeys: Failure responding to request: StatusCode=429 -- Original Error: autorest/azure: Service returned an error. Status=429 Code="TooManyRequests" Message="The request is being throttled as the limit has been reached for operation type - Read_ObservationWindow_00:05:00. For more information, see - https://aka.ms/srpthrottlinglimits\"" error.file="/go/src/velero-plugin-for-microsoft-azure/velero-plugin-for-microsoft-azure/object_store.go:217" error.function=main.getStorageAccountKey key=velero/test7feb logSource="pkg/controller/backup_controller.go:300"
time="2023-02-07T08:13:39Z" level=info msg="Validating BackupStorageLocation" backup-storage-location=velero/default controller=backup-storage-location logSource="pkg/controller/backup_storage_location_controller.go:131"
time="2023-02-07T08:13:39Z" level=info msg="BackupStorageLocations is valid, marking as available" backup-storage-location=velero/default controller=backup-storage-location logSource="pkg/controller/backup_storage_location_controller.go:116"
time="2023-02-07T08:13:39Z" level=error msg="Current BackupStorageLocations available/unavailable/unknown: 0/1/0)" controller=backup-storage-location logSource="pkg/controller/backup_storage_location_controller.go:173"
time="2023-02-07T08:13:39Z" level=info msg="Found 27 backups in the backup location that do not exist in the cluster and need to be synced" backupLocation=default controller=backup-sync logSource="pkg/controller/backup_sync_controller.go:211"
time="2023-02-07T08:13:39Z" level=info msg="Attempting to sync backup into cluster" backup=velero-daily-20230127030044 backupLocation=default controller=backup-sync logSource="pkg/controller/backup_sync_controller.go:219"
time="2023-02-07T08:13:39Z" level=info msg="Successfully synced backup into cluster" backup=velero-daily-20230127030044 backupLocation=default controller=backup-sync logSource="pkg/controller/backup_sync_controller.go:249"

�]0;root@UK-AZR-PUSREJ01: ~�root@UK-AZR-PUSREJ01
�]0;root@UK-AZR-PUSREJ01: �root@UK-AZR-PUSREJ01:# velero backup describe test7feb2
Name: �[1mtest7feb2�[0m
Namespace: velero
Labels: velero.io/storage-location=default
Annotations: velero.io/source-cluster-k8s-gitversion=v1.23.12
velero.io/source-cluster-k8s-major-version=1
velero.io/source-cluster-k8s-minor-version=23

Phase: �[31mFailed�[0m (run velero backup logs test7feb2 for more information)

Errors: 0
Warnings: 0

Namespaces:
Included: *
Excluded:

Resources:
Included: *
Excluded:
Cluster-scoped: auto

Label selector:

Storage Location: default

Velero-Native Snapshot PVs: auto

TTL: 720h0m0s

Hooks:

Backup Format Version:

Started: 2023-02-07 08:15:49 +0000 UTC
Completed: <n/a>

Expiration: 2023-03-09 08:15:49 +0000 UTC

Velero-Native Snapshots:
�]0;root@UK-AZR-PUSREJ01: �root@UK-AZR-PUSREJ01:#
�]0;root@UK-AZR-PUSREJ01: �root@UK-AZR-PUSREJ01:#
�]0;root@UK-AZR-PUSREJ01: �root@UK-AZR-PUSREJ01:#
�]0;root@UK-AZR-PUSREJ01: �root@UK-AZR-PUSREJ01:# k logs restic-2sskk -n velero
time="2023-02-07T08:10:42Z" level=info msg="Setting log-level to INFO"
time="2023-02-07T08:10:42Z" level=info msg="Starting Velero restic server v1.9.5 (2b5281f38aad2527f95b55644b20fb169a6702a7-dirty)" logSource="pkg/cmd/cli/restic/server.go:87"
1.675757442435557e+09 INFO controller-runtime.metrics Metrics server is starting to listen {"addr": ":8080"}
time="2023-02-07T08:10:42Z" level=info msg="Starting metric server for restic at address [:8085]" logSource="pkg/cmd/cli/restic/server.go:177"
time="2023-02-07T08:10:42Z" level=info msg="Starting controllers" logSource="pkg/cmd/cli/restic/server.go:188"
time="2023-02-07T08:10:42Z" level=info msg="Controllers starting..." logSource="pkg/cmd/cli/restic/server.go:219"
1.6757574425062695e+09 INFO Starting server {"path": "/metrics", "kind": "metrics", "addr": "[::]:8080"}
1.6757574425064323e+09 INFO Starting EventSource {"controller": "podvolumebackup", "controllerGroup": "velero.io", "controllerKind": "PodVolumeBackup", "source": "kind source: *v1.PodVolumeBackup"}
1.675757442506599e+09 INFO Starting Controller {"controller": "podvolumebackup", "controllerGroup": "velero.io", "controllerKind": "PodVolumeBackup"}
1.675757442506474e+09 INFO Starting EventSource {"controller": "podvolumerestore", "controllerGroup": "velero.io", "controllerKind": "PodVolumeRestore", "source": "kind source: *v1.PodVolumeRestore"}
1.675757442506642e+09 INFO Starting EventSource {"controller": "podvolumerestore", "controllerGroup": "velero.io", "controllerKind": "PodVolumeRestore", "source": "kind source: *v1.Pod"}
1.6757574425066628e+09 INFO Starting Controller {"controller": "podvolumerestore", "controllerGroup": "velero.io", "controllerKind": "PodVolumeRestore"}
1.6757574426075783e+09 INFO Starting workers {"controller": "podvolumebackup", "controllerGroup": "velero.io", "controllerKind": "PodVolumeBackup", "worker count": 1}
1.6757574426076603e+09 INFO Starting workers {"controller": "podvolumerestore", "controllerGroup": "velero.io", "controllerKind": "PodVolumeRestore", "worker count": 1}
�]0;root@UK-AZR-PUSREJ01: �root@UK-AZR-PUSREJ01:#
�]0;root@UK-AZR-PUSREJ01: �root@UK-AZR-PUSREJ01:#
�]0;root@UK-AZR-PUSREJ01: �root@UK-AZR-PUSREJ01:#
�]0;root@UK-AZR-PUSREJ01: �root@UK-AZR-PUSREJ01:#
�]0;root@UK-AZR-PUSREJ01: �root@UK-AZR-PUSREJ01:#
�]0;root@UK-AZR-PUSREJ01: �root@UK-AZR-PUSREJ01:# k logs restic-2sskk -n velero ��������������[C�[C�������������[12P�[12@restic-bfkjh
time="2023-02-07T08:10:38Z" level=info msg="Starting Velero restic server v1.9.5 (2b5281f38aad2527f95b55644b20fb169a6702a7-dirty)" logSource="pkg/cmd/cli/restic/server.go:87"
time="2023-02-07T08:10:38Z" level=info msg="Setting log-level to INFO"
1.675757438543832e+09 INFO controller-runtime.metrics Metrics server is starting to listen {"addr": ":8080"}
time="2023-02-07T08:10:38Z" level=info msg="Starting metric server for restic at address [:8085]" logSource="pkg/cmd/cli/restic/server.go:177"
time="2023-02-07T08:10:38Z" level=info msg="Starting controllers" logSource="pkg/cmd/cli/restic/server.go:188"
time="2023-02-07T08:10:38Z" level=info msg="Controllers starting..." logSource="pkg/cmd/cli/restic/server.go:219"
1.6757574386095107e+09 INFO Starting server {"path": "/metrics", "kind": "metrics", "addr": "[::]:8080"}
1.6757574386096985e+09 INFO Starting EventSource {"controller": "podvolumebackup", "controllerGroup": "velero.io", "controllerKind": "PodVolumeBackup", "source": "kind source: *v1.PodVolumeBackup"}
1.675757438609769e+09 INFO Starting Controller {"controller": "podvolumebackup", "controllerGroup": "velero.io", "controllerKind": "PodVolumeBackup"}
1.675757438609736e+09 INFO Starting EventSource {"controller": "podvolumerestore", "controllerGroup": "velero.io", "controllerKind": "PodVolumeRestore", "source": "kind source: *v1.PodVolumeRestore"}
1.6757574386098542e+09 INFO Starting EventSource {"controller": "podvolumerestore", "controllerGroup": "velero.io", "controllerKind": "PodVolumeRestore", "source": "kind source: *v1.Pod"}
1.6757574386098726e+09 INFO Starting Controller {"controller": "podvolumerestore", "controllerGroup": "velero.io", "controllerKind": "PodVolumeRestore"}
1.6757574387107615e+09 INFO Starting workers {"controller": "podvolumebackup", "controllerGroup": "velero.io", "controllerKind": "PodVolumeBackup", "worker count": 1}
1.6757574387107272e+09 INFO Starting workers {"controller": "podvolumerestore", "controllerGroup": "velero.io", "controllerKind": "PodVolumeRestore", "worker count": 1}
�]0;root@UK-AZR-PUSREJ01: �root@UK-AZR-PUSREJ01:#
�]0;root@UK-AZR-PUSREJ01: �root@UK-AZR-PUSREJ01:#
�]0;root@UK-AZR-PUSREJ01: �root@UK-AZR-PUSREJ01:#
�]0;root@UK-AZR-PUSREJ01: �root@UK-AZR-PUSREJ01:# k logs restic-bfkjh -n velero ������������������������[12P�[13@restic-x5v5f
time="2023-02-07T08:10:40Z" level=info msg="Starting Velero restic server v1.9.5 (2b5281f38aad2527f95b55644b20fb169a6702a7-dirty)" logSource="pkg/cmd/cli/restic/server.go:87"
time="2023-02-07T08:10:40Z" level=info msg="Setting log-level to INFO"
1.6757574406452508e+09 INFO controller-runtime.metrics Metrics server is starting to listen {"addr": ":8080"}
time="2023-02-07T08:10:40Z" level=info msg="Starting metric server for restic at address [:8085]" logSource="pkg/cmd/cli/restic/server.go:177"
time="2023-02-07T08:10:40Z" level=info msg="Starting controllers" logSource="pkg/cmd/cli/restic/server.go:188"
time="2023-02-07T08:10:40Z" level=info msg="Controllers starting..." logSource="pkg/cmd/cli/restic/server.go:219"
1.675757440743646e+09 INFO Starting server {"path": "/metrics", "kind": "metrics", "addr": "[::]:8080"}
1.675757440743859e+09 INFO Starting EventSource {"controller": "podvolumebackup", "controllerGroup": "velero.io", "controllerKind": "PodVolumeBackup", "source": "kind source: *v1.PodVolumeBackup"}
1.675757440743913e+09 INFO Starting Controller {"controller": "podvolumebackup", "controllerGroup": "velero.io", "controllerKind": "PodVolumeBackup"}
1.6757574407440953e+09 INFO Starting EventSource {"controller": "podvolumerestore", "controllerGroup": "velero.io", "controllerKind": "PodVolumeRestore", "source": "kind source: *v1.PodVolumeRestore"}
1.6757574407441623e+09 INFO Starting EventSource {"controller": "podvolumerestore", "controllerGroup": "velero.io", "controllerKind": "PodVolumeRestore", "source": "kind source: *v1.Pod"}
1.6757574407441702e+09 INFO Starting Controller {"controller": "podvolumerestore", "controllerGroup": "velero.io", "controllerKind": "PodVolumeRestore"}
1.6757574408453553e+09 INFO Starting workers {"controller": "podvolumebackup", "controllerGroup": "velero.io", "controllerKind": "PodVolumeBackup", "worker count": 1}
1.6757574408454797e+09 INFO Starting workers {"controller": "podvolumerestore", "controllerGroup": "velero.io", "controllerKind": "PodVolumeRestore", "worker count": 1}
�]0;root@UK-AZR-PUSREJ01: �root@UK-AZR-PUSREJ01:#
