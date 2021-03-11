ssh-key: The directory is to copy ssh-key to any number of nodes.

Weather: This Directory helps us to check the weather of the city

oc adm certificate approve `oc get csr -o=jsonpath={.items[*].metadata.name}`

95a03d9ba8611809d6228adb7582878a35ebbaab

index= sourcetype="*" host= |eval raw_len=len(_raw) | eval raw_len_gb=raw_len/1024/1024/1024 |stats sum(raw_len_gb) as GB by sourcetype
