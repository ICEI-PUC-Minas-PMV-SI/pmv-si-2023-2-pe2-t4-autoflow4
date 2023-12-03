# Artefatos relativos à modelagem de dados do projeto

Este diretório mantém os artefatos relacionados à modelagem de dados do projeto. 


* `diagrama entidade-relacionamento (DER)`
<p align="center">
  <img src="imagens_modelo\Diagrama-Entidade.svg" alt="AutoFlowlogo">
</p>

# Impactos da implementação em um banco de dados NoSQL

A modelagem de banco de dados proposta possui simplicidade sobre as operações, porém pode requisitar um alto volume de dados cadastrados em pouco tempo, além das relações internas serem extremamente relevantes entre seus dados. Considerando que um mesmo veículo vai ter, ao longo do tempo, altos registros de relatórios de aluguel, por exemplo, é essencial que o banco tolere esse alto volume de entradas e mantenha a viabilidade das operações de locação dos veículos, mas também tenha consistência desses dados para busca.
Bancos de dados NoSQL possuem um modelo de dados orientado por agregados como unidade mínima. Isso trás a possibilidade de escalonamento horizontal e de processamento paralelizado dos dados, o que possibilita resistência ao alto volume de consultas e coopera em uma disponibilidade mais resiliente dessas informações. Apesar disso, eles não possuem transações, sendo sua consistência garantida somente pela estratégia de versionamento, o que gera complexidade nas consultas e não necessariamente supre as necessidades em casos de relações muito relevantes nas buscas.
Nosso contexto requer uma alta consistência de dados, visto que a atualização dos relatórios, status do veículo e data de pickup e dropout são altamente relevantes para o negócio. A disponibilidade desses dados também é relevante, visto que ajuda a garantir que as operações dos atendentes sejam realizadas com sucesso. 
As operações requisitadas para locação de veículos são majoritariamente a persistência de dados para consulta, ou seja, dados permanentes. Além disso, o cruzamento desses dados simultâneos é relevante para a consistência sobre a busca de aluguéis de veículos. Por isso, a opção de um banco SQL se torna interessante, mantendo a consistência e a avaliabilidade desses dados. O banco de dados postgres é um banco relacional de alta performance e será nossa base.
 

* `modelo relacional`
<p align="center">
  <img src="imagens_modelo\Diagrama-Modelo-Relacional.svg" alt="AutoFlowlogo">
</p>



-----------------------------------------

# Valores das entidades

| Entidade          | Valores                                       |
|-------------------|-----------------------------------------------|
| Status do veículo | Disponível, Reservado, Manutenção              |
| Status do aluguel  | Reservado, Aguardando Retirada, Documentação pendente, Em atraso, Aguardando devolução, Finalizado |
| Categoria do veículo | Hatch, Sedan, Utilitário, SUV                  |
| Status IPVA       | Vigente, Vencido                               |
| Status Seguro     | Vigente                                       |
