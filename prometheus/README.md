# Instalação

Para instalação do Prometheus, utilizarei um Helm Chart bem conhecido chamado `kube-prometheus-stack`, que instala
alguns Charts como dependência e já prepara o ambiente, como dashboards para o Grafana, uma aplicação para visualizarmos
os gráficos com os dados do Prometheus.
Também utilizamos um outro chart chamado `prometheus-adapter`, este sendo
necessário para utilizarmos métricas customizadas, facilitando no uso do Grafana para ter gráficos melhores.

Para isto iniciaremos instalando o Chart na nossa máquina

## Instalando repositório

```
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
```

## Baixando e atualizando dependências

Devemos criar as dependencias para podermos instalar o Chart via

```
helm dependency build
```

Para atualizar as dependências, é necessário editar o arquivo Chart.yaml para atualizar as versões, e em seguida executar o comando

```
helm dependency update
```

## Instalando Chart

Utilizaremos como nome da release `default`, permitindo que tenhamos mais de uma instalação e informando que
esta será a instalação padrão que utilizaremos para todo o cluster.

```
helm upgrade --install default --namespace prometheus --values values.override.yaml \
    --create-namespace --debug --wait --cleanup-on-fail .
```
