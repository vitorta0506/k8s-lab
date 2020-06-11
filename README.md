## Tshoot nodes K8S

### Verificar se todos os pods estão rodando corretamente:
kubectl get pods --all-namespaces

O comando abaixo da uma visão geral de todos os recursos que estão rodando:

watch kubectl get all --all-namespaces

### Caso tenha erro em algum pod vamos dar um describe para verificar o motivo do erro:
kubectl describe pod -n kube-system <nome de pod>

Ficar atento ao namespace pois se não informar nenhum pode ser que de erro dizendo que o pod nao existe.

Analisar os logs e dar uma googada no erro e ir documentando.

Peguei um erro onde os nodes nao ficavam ready, identifiquei que os pods do kube-proxy não ficavam running e consequentemente os pods de Network tb não ficavam. O erro apresentado no log do pod era o seguinte:

"failed to start container "kube-proxy": Error response from daemon: error while creating mount source path......"

Perdi 1 dia tentando identificar o motivo do erro, depois de algumas pesquisas vi um problema parecido onde falavam que tiveram problema com a instalação do docker via script(curl -fsSL https://get.docker.com), nesse caso removi a instalação do docker e refiz via apt-get após isso ingressei novamente os nodes no cluster e os mesmos ficaram ready.

