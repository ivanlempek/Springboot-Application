# API Rest - Parking Spot

Dependências:

  -JDK 14
  -postgresql
  -postman
  -maven
  
---------------------------------------------------

Descrição da aplicação:

Uma API de cadastro de vaga de estacionamento com banco de dados PostgreSQL.

Podemos inserir uma vaga com os seguintes atributos:

	-número da vaga;
	-placa do carro;
	-marca do carro;
	-modelo do carro;
	-nome do responsável;
	-apartamento;
	-bloco.

Todos os atributos passados pelo usuário são verificados por diversas validações, fazendo assim que nenhum dado possa ficar em branco na hora do registro.
O id e a data de registro da vaga cadastrada são gerados automaticamente. Lembrando que a data de registro foi alterada para UTC.

A API pode ser usada com o Postman e foi feita para rodar com os métodos POST,GET,PUT e DELELTE.
A aplicação possui também paginação que informa o número de elementos registrados por página, número de páginas,etc.

---------------------------------------------------

Levantando a API

Postgree:

- Conectamos nossa api com o banco inserindo o user e senha do postgre dentro de application.properties:
    -spring.datasource.username=postgres
    -spring.datasource.password=123456
- Criamos um banco dentro do pgadmin do postgree chamado "parking-control-db".
- Depois de levantar a aplicação verificamos se a tabela "tb_parking_spot" foi criada.


Postman:
- Adicionamos cada método (POST,GET,DELETE,UPDATE).
- Dentro do postman, utilizando o métododo POST com a URI http://localhost:8080/parking-spot, vamos em body, raw e adicionamos os campos que vão ser salvos:

	{
    		"parkingSpotNumber": "205B",
		"licensePlateCar": "RRS8562",
    		"brandCar": "audi",
    		"modelCar": "q5",
    		"colorCar": "black",
    		"responsibleName": "Carlos Daniel",
    		"apartment": "220",
    		"block": "D"
	}

- Após enviar os dados deverá ser retornado um "201 Created" com todos os dados mais o Id e o registrationDate inclusos.
- Tabém poderá ser feito as verificações caso ocorra repetições dos campos de placa, número de vaga, apartamento ou bloco. Retornando uma mensagem de conflito.

Agora podemos criar e visualizar todos os registros feitos com o método GET utilizando o mesmo URI: http://localhost:8080/parking-spot

Podemos agora testar também:
	- o GET por id: http://localhost:8080/parking-spot/id
	- o DELETE por id: http://localhost:8080/parking-spot/id 
	- o PUT por id: http://localhost:8080/parking-spot/id 

Além disso, temos também a paginação (dentro do get de todos os elementos):
	- pode-se testar ela inserindo um 'key' page dentro do postman com o valor 0 para retornar a primeira página, valor 1 para a segunda página e vice-versa.
	- pode-se testar também definindo um 'key' size para limitar o número de elementos por página.
	- e por fim, pode-se fazer também ordernar por data de registro, sendo um 'key' do tipo 'sort' com os valores de 'registrationDate,ASC' ou 'registrationDate,DESC' 

	
