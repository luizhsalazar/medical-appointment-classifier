# Aprendizado Supervisionado
## Projeto: Previsão de comparecimento do paciente na consulta agendada

### [DEMO](https://pablozandona.github.io/medical-appointment-classifier/)

### Instalação

O projeto requer o **Python 3*** e as seguintes bibliotecas instaladas:

- [NumPy](http://www.numpy.org/)
- [Pandas](http://pandas.pydata.org)
- [scikit-learn](http://scikit-learn.org/stable/)

### Código

O código do classificador está disponível no arquivo `ml/classifier.py` e o código responsável para a geração do modelo está no arquivo `ml/builder.py`. Para geração do modelo será necessário a inclusão do arquivo `data/medical_appointment.csv` para treinamento e teste do modelo.

### Execução

Em um terminal, navegue até a raiz do diretório do projeto `medical-appointment-classifier/ml` e execute o comando:

```bash
python builder.py
```  

A execução deste código irá realizar os seguintes passos:

1. Dividir dos dados em dois conjuntos: Atributos e Classes
2. Dividir os dados aleatoriamente em conjunto para aprendizado e conjunto para testes
3. Treinar o modelo
    * Modelo `Decision Tree`
    * Modelo `Random Forest`
4. Aplicar o modelo gerado sobre os dados separados para testes
5. Avaliar o modelo 
    * Cálcular a acurácia do modelo
    * Gerar a matriz de contingência
    * Calcular a especificidade e a sensibilidade do modelo
6. Salvar o modelo para uso posterior

### Dados

O dataset consiste de aproximadamente 110.500 agendamentos de consulta médicas, sendo que cada datapoint é constituído de 14 características associadas. Os dados foram originalmente extraídos através do portal de [dados do governo](http://dados.gov.br/) e são de hospitais públicos da cidade de Vitória, no estado do Espírito Santo. A amostra de dados é dos anos de 2015 e 2016, tanto dos agendamentos quanto dos dias da consulta. Os dados foram retirados do dataset [Medical Appointment No Shows](https://www.kaggle.com/joniarroba/noshowappointments) do repositório do `Kaggle`.

**Atributos (features)**
- `PatientId`: Identificador do paciente
- `AppointmentID`: Identificador do agendamento da consulta
- `Gender`: Gênero do paciente
- `ScheduledDay`: Data do agendamento da consulta
- `AppointmentDay`: Data da consulta 
- `Age`: Idade do paciente
- `Neighbourhood`: Bairro de Vitória em que o paciente reside
- `Scholarship`: Pacente beneficiário do programa do governo `Bolsa Família` (1 ou 0)
- `Hipertension`: Paciente hipertenso (1 ou 0)
- `Diabetes`: Paciente diabético (1 ou 0)
- `Alcoholism`: Paciente alcoólatra (1 ou 0)
- `Handcap`: Paciente com necessidades especiais (1 ou 0)
- `SMS_received`: Paciente recebeu mensagem SMS antes da consulta (1 ou 0)

**Classes (target variable)**
- `No-show`: Paciente compareceu a consulta no dia agendado (1 ou 0)

### API + Frontend da Aplicação

Para viabilizar o teste do modelo gerado com maior facilidade foi implementada uma API REST. O microframework `Flask` foi utilizado para a criação do endpoint da aplicação. O código implementado pode ser visualizado no arquivo `app.py` na raiz do projeto. Já no frontend, o framework `Vue.js` foi utilizado para disponibilizar a inserção dos dados pelo usuário via interface. A API desenvolvida possui um método `predict` que recebe requisições POST com os parâmetros de entrada. Os parâmetros são transformados para o padrão de dados aceito pelo modelo e são inseridos como input no modelo de machine learning desenvolvido.

### Deploy e Limitações

O projeto foi implantando no ecossistema de nuvem `Heroku`. Os arquivos de configuração para deploy estão localizados na raiz do projeto. A principal limitação da versão implantada é o delay que pode ser ocasionado para obtenção de respostas do servidor. Isto deve-se ao fato da versão free ter a limitação na qual a aplicação "dorme" a cada 30 minutos de inatividade.
