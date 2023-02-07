Would like to know the reason behind sudden failure of Velero backup in our Azure Kubernetes cluster.

Pasting the import gist of command output followed by,

kubectl logs deployment/velero -n velero

velero backup describe or kubectl get backup/ -n velero -o yaml

velero backup logs

k logs <velero_pod> -n velero

(https://github.com/RJ-Kamalesh/Velero_Partially-Failed/files/10674316/eastus_vto.txt) 


Environment:

Velero version (use velero version) : v1.9.5

Microsoft plugins of velero : v1.5.3

Kubernetes version : Server version v1.23.12 , Client version v1.23.4

Cloud Provider : Azure

 <img width="509" alt="velero_get_backup" src="https://user-images.githubusercontent.com/124659220/217228730-188a6ce8-fa34-466a-9017-46f74305707b.PNG">


<img width="381" alt="describe_backup" src="https://user-images.githubusercontent.com/124659220/217230924-fb8bbd60-ea9a-4569-91ea-89fd4c499c30.PNG">


<img width="636" alt="velero_logs_errors" src="https://user-images.githubusercontent.com/124659220/217235571-e513c65c-3849-492b-b4da-bc94653d7747.PNG">

Above highlighted Errors as:

- The request is being throttled as the limit has been reached for operation type - Read_ObservationWindow_00:05:00. For more information, see - https://aka.ms/srpthrottlinglimits\"" error.file="/go/src/velero-plugin-for-microsoft-azure/velero-plugin-for-microsoft-azure/object_store.go:217" error.function=main.getStorageAccountKey key=velero/test7feb logSource="pkg/controller/backup_controller.go:300"
time="2023-02-07T08:13:39Z" level=info msg="Validating BackupStorageLocation" backup-storage-location=velero/default controller=backup-storage-location 

- time="2023-02-07T08:12:57Z" level=info msg="BackupStorageLocation is invalid, marking as unavailable" backup-storage-location=velero/default controller=backup-storage-location logSource="pkg/controller/backup_storage_location_controller.go:110"

- time="2023-02-07T08:13:39Z" level=error msg="Current BackupStorageLocations available/unavailable/unknown: 0/1/0)" controller=backup-storage-location 



<img width="676" alt="restic_logs" src="https://user-images.githubusercontent.com/124659220/217238997-3c5fde97-7095-4bb6-bb57-1b9a2677dc60.PNG">
