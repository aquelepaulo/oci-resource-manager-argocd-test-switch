# Argo CD no OKE: TESTE 1 para TESTE 2

Aplicação GitOps para a apresentação **"Saiba como automatizar sua infraestrutura com Terraform OCI Provider, Resource Manager e Argo CD"**.

O Resource Manager já foi usado para a infraestrutura OCI. Este repositório trata exclusivamente do segundo ato: GitOps. O Argo CD, já instalado no OKE existente, observa este repositório, cria o `Deployment`, `Service` e `ConfigMap` e reconcilia qualquer alteração em Git. Não há `kubectl apply` da aplicação depois do bootstrap.

## Limite intencional

O cluster OKE e a Stack do Resource Manager já existem e estão fora do escopo deste repositório.

## Roteiro da apresentação

1. Publique este repositório em GitHub/GitLab **público**. Para Git privado, configure no Argo CD um Secret de repositório; não inclua token no manifesto.
2. No Cloud Shell, aplique `argocd/application.yaml`. Aguarde `test-switch` ficar `Synced` e `Healthy`.
3. Obtenha o endereço público com `kubectl -n gitops-demo get svc test-switch` e execute `curl "http://<EXTERNAL-IP>/"`. O retorno é `TESTE 1`.
5. Em `kubernetes/app/default.conf`, altere somente `TESTE 1` para `TESTE 2`; faça commit e push para `main`.
6. No Argo CD, mostre o novo commit, a aplicação `OutOfSync` e a sincronização automática. Para não esperar o ciclo de reconciliação, use **Sync** na UI do Argo CD.
7. Execute novamente o mesmo `curl`. Agora o retorno é `TESTE 2`.

## Por que o endpoint muda sem um novo `kubectl apply`?

O `configMapGenerator` gera um novo nome de ConfigMap quando `default.conf` muda. Essa referência altera o template do Deployment e o Kubernetes faz um rollout. Argo CD é quem aplica essa mudança porque Git é a fonte de verdade.

## Aplicar a Application

```sh
kubectl apply -f argocd/application.yaml
```

## Fontes

- [Argo CD automated sync](https://argo-cd.readthedocs.io/en/stable/user-guide/auto_sync/)
