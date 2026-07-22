# Script falado — 7 minutos

**0:00 — Problema.** "Infra e aplicação não precisam ter o mesmo controlador. O Resource Manager mantém o estado da infraestrutura OCI; Argo CD mantém o estado Kubernetes declarado em Git."

**0:45 — IaC.** Mostre a Stack do Resource Manager já concluída e explique que o OKE já existe para a demo. Este repositório começa no estado desejado da aplicação.

**1:45 — Estado desejado.** Mostre `kubernetes/app/`: Deployment, Service e o arquivo `default.conf`. Destaque que o endpoint atualmente declara `TESTE 1`.

**2:30 — GitOps.** Mostre a `Application` do Argo CD: repositório, caminho `kubernetes/app`, `automated`, `prune` e `selfHeal`.

**3:15 — Prova 1.** Execute `curl "<demo_endpoint>"` e mostre `TESTE 1`.

**4:00 — Mudança.** Altere apenas `TESTE 1` para `TESTE 2`, faça commit e push. Não execute `kubectl apply`.

**4:45 — Reconciliação.** Mostre o commit detectado e o sync no Argo CD; mostre o novo ReplicaSet ou o rollout concluído.

**5:45 — Prova 2.** Execute o mesmo curl e mostre `TESTE 2`.

**6:15 — Fecho.** "Terraform/Resource Manager trata da base OCI e do estado Terraform; Git declara a aplicação; Argo CD continuamente torna o cluster igual a Git."
