# Aula: Trabalhando com Machine Learning na Prática no Azure ML

Passo a passo do projeto Trabalhando com Machine Learning na Prática no Azure ML da DIO.

Links importantes:

[Explore Azure AI Services](https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/02-content-safety.html)

[Explore Automated Machine Learning in Azure Machine Learning](https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/01-machine-learning.html)

[Fonte dos dados](https://aka.ms/bike-rentals)

## Passo 1: Criando a área de trabalho (workspace) para o Azure Machine Learning

Entrar no portal.zure.com e clicar em "Criar recurso", pesquisar por Azure Machine Learning no marketplace e selecionar para criar.

![Img](./imgs/img001.png)

![Img](./imgs/img002.png)

![Img](./imgs/img003.png)

## Passo 2: Configurando o workspace do Azure Machine Learning

Para configurar este recurso, é necessário informar:
* um grupo de recursos (resource group). No caso dei o nome de LABAI-900.
* a localização geográfica. Como sugestão, selecionar East US por ser próximo, além de geralmente ser mais barato do que no Brasil.
* informar a assinatura (subscription), que neste caso estamos usando a Avaliação Gratuita de $200.
* Nas próximas abas, dá para deixar tudo default da ferramenta, passar pela validação e criar o recurso. Estilo next-> next-> finish.
* Após a criação, clicar no botão Go to resource. Nesta página, clicar no botão Lauch studio, que abrirá o Machine Learning Studio (ml.azure.com).

![Img](./imgs/img004.png)

![Img](./imgs/img005.png)

![Img](./imgs/img006.png)

![Img](./imgs/img007.png)

![Img](./imgs/img008.png)

## Passo 3 - Criando um aprendizado de máquina automatizado (Automated ML) para treinar o modelo

No estúdio, na página do workspace criado anteriormente, acessei a opção do menu ML automatizado e na página aberto, cliquei em "Novo trabalho de ML automatizado".

![Img](./imgs/img5.gif)

Em "Configurações básicas", preenchi os campos "Nome do trabalho", "Novo nome do experimento" e "Descrição". Após cliquei em "Avançar".

No passo "Tipo de tarefa e dados", selecionei o tipo de tarefa como Regressão e em seguida, em "Selecionar dados", cliquei em "Criar". No modal aberto, em "Tipos de dados", preenchi os campos "Nome", "Descrição" e escolhi "Tipo" como Tabular. Cliquei em "Avançar" e no passo "Fonte de dados", escolhi "De arquivos da Web" e cliquei em avançar novamente.

No passo "URL da Web", informei a URL [https://aka.ms/bike-rentals](https://aka.ms/bike-rentals) do conjunto de dados. Algumas vezes tive problemas com a validação dos dados, então usei essa URL: [https://raw.githubusercontent.com/MicrosoftLearning/mslearn-ai-fundamentals/main/data/ml/daily-bike-share.csv](https://raw.githubusercontent.com/MicrosoftLearning/mslearn-ai-fundamentals/main/data/ml/daily-bike-share.csv). No passo "Configurações", preenchi as configurações do conjunto e após avançar para "Esquema", verifiquei os tipos de dados. Finalmente, ao avançar, verifiquei as configurações criadas para o ativo de dados e cliquei em criar.

![Img](./imgs/img6.gif)

Em "Configurações de tarefas", escolhi o conjunto de dados importado. Após, em "Coluna de destino" escolhi a coluna rentals como target.

Nos campos de "Limite", preenchi com os valores abaixo e marquei "Habilitar encerramento antecipado".

![Img](./imgs/img7.png)

Em "Validar e testar", em "Tipo de validação" escolhi "Divisão de validação de treinamento".

Ao avançar, em Computação, mantive os valores mostrados na imagem abaixo.

![Img](./imgs/img8.png)

Após avançar e examinar as configurações do trabalho, cliquei em "Enviar trabalho de treinamento".

Após finalizar o trabalho de treinamento, precisei criar o modelo. Para isso, acessei a página do trabalho realizado e cliquei em "Modelo de registro". Deixei as opções padrões para "Selecionar saída". Em "Configurações do modelo", somente preenchi o nome e a versão. Após isso, cliquei em criar o modelo.

![Img](./imgs/img12.gif)

Po fim, o modelo fica acessível na opção de menu "Modelo".

![Img](./imgs/img9.png)

## Passo 4: Métricas do modelo

Para acessar as métricas do modelo treinado, na página do modelo, acesso o link informado em "Criado por trabalho". Também é possível acessar o trabalho informado na opção do menu "Tarefas (jobs)".

Na página da tarefa, acessei a aba métricas.

![Img](./imgs/img10.gif)

## Passo 5: Teste do modelo

Na página do modelo, acessei a aba "Pontos de extremidade" e em seguida cliquei em "Implantar". Porém, por algum motivo o botão não funcionou. Então, para criar o ponto de extremidade para esse modelo, acessei "Pontos de extremidade" no menu lateral, e cliquei em "Criar". Em seguida marquei o modelo e deixei todos os campos seguintes como os valores padrões, exceto "Contagem de instâncias" que deixei como 1. Então cliquei em "Implantar".

![Img](./imgs/img13.gif)

Logo após a implantação, que demora bastante, acessei a aba "Testar" do ponto de extremidade criado para o meu modelo.

Para o teste, utilizei o json abaixo:

<code>
{
  "input_data": {
    "data": [
       {
         "day": 1,
         "mnth": 1,   
         "year": 2022,
         "season": 2,
         "holiday": 0,
         "weekday": 1,
         "workingday": 1,
         "weathersit": 2, 
         "temp": 0.3, 
         "atemp": 0.3,
         "hum": 0.3,
         "windspeed": 0.3 
       }
     ]
  }
}
</code>

A previsão gerada foi: 347.73

![Img](./imgs/img11.png)
