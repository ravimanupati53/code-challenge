ssh-key: The directory is to copy ssh-key to any number of nodes.

Weather: This Directory helps us to check the weather of the city

oc adm certificate approve `oc get csr -o=jsonpath={.items[*].metadata.name}`


index= sourcetype="*" host= |eval raw_len=len(_raw) | eval raw_len_gb=raw_len/1024/1024/1024 |stats sum(raw_len_gb) as GB by sourcetype
