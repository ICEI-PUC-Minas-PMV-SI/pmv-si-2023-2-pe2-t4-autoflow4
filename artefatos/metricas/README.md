# Relatórios Analíticos


Essa seleção de relatórios foi elaborada para fornecer informações detalhadas sobre os processos essenciais de gerenciamento de clientes, veículos e reservas. Ao focar em aspectos específicos, como clientes ativos, rendimento veicular e uso mensal de veículos por cliente, esses relatórios visam oferecer insights cruciais para aprimorar a eficiência operacional e apoiar decisões estratégicas na gestão dessas áreas-chave.

| **Processo**              | **Relatório**                              | **Descrição**                                                                   |
| -------------------------- | ------------------------------------------ | --------------------------------------------------------------------------------- |
| Gerenciar Clientes         | Relatório de Clientes Ativos               | Mostra a lista de clientes ativos.                                              |
|                            | Relatório Mensal de Clientes Ativos        | Apresenta uma visão mensal da evolução do número de clientes ativos.            |
| Gerenciar Veículos         | Relatório de Média de Rendimento por Veículo | Calcula a média de rendimento para cada veículo gerenciado.                      |
|                            | Relatório de Lucro por Modelo              | Apresenta o lucro gerado por cada modelo de veículo, oferecendo uma visão financeira adicional à gestão da frota. |
| Reserva de Veículo         | Relatório Mensal de Uso de Veículo por Cliente | Detalha o uso mensal de veículos por cada cliente, destacando reservas e atividades. |


# Associação de comandos SQL com Relatórios Analíticos



- **Relatório de Clientes Ativos**

<p align="center">
  <img src="analytics\Analytics - Relatorio clientes ativos.jpg" alt="AutoFlowlogo">
</p>

**Comando SQL-DML (SELECT):**

    SELECT cliente_selecionado, data_conclusao,
           COUNT(cliente_selecionado) AS gerenciar_clientes_turma_4_veiculo
    FROM Gerenciar_clientes
    GROUP BY cliente_selecionado, data_conclusao;


- **Relatório Mensal de Clientes Ativos:**
  
<p align="center">
  <img src="analytics\Analytics - Relatorio mensal de Clientes Ativos.jpg" alt="AutoFlowlogo">
</p>

**Comando SQL-DML (SELECT):**

    SELECT cliente.nome, veiculo.modelo, veiculo.placa, status
    FROM aluguel
    JOIN cliente ON aluguel.ID_CLIENTE = cliente.ID
    JOIN veiculo ON aluguel.ID_VEICULO = veiculo.ID
    WHERE status != 'Finalizado';


- **Relatório Média de Rendimento por Veículo:**

<p align="center">
  <img src="analytics\Analytics - Relatorio media de rendimento por veiculo.jpg" alt="AutoFlowlogo">
</p>

**Comando SQL-DML (SELECT):**

    SELECT veiculo.modelo, AVG(VALOR)
    FROM aluguel
    JOIN veiculo ON aluguel.id_veiculo
    GROUP BY veiculo.modelo;

- **Relatório de Lucro por Modelo:**

<p align="center">
  <img src="analytics\Analytics - Relatorio de lucro por modelo.jpg" alt="AutoFlowlogo">
</p>

**Comando SQL-DML (SELECT):**

    SELECT veiculo.modelo, SUM(valor) AS total_valor
    FROM aluguel
    JOIN veiculo ON aluguel.ID_VEICULO = veiculo.ID;

- **Relatório Mensal de uso de Veículo por Cliente:**

<p align="center">
  <img src="analytics\Analytics - Relatorio mensal de uso de veiculo por cliente.jpg" alt="AutoFlowlogo">
</p>

**Comando SQL-DML (SELECT):**

    SELECT veiculo.modelo, cliente.nome, strftime('%m', data_reserva) AS mes, SUM(valor) AS total_valor
    FROM aluguel
    JOIN cliente ON aluguel.ID_CLIENTE = cliente.ID
    JOIN veiculo ON aluguel.ID_VEICULO = veiculo.ID
    GROUP BY veiculo.modelo, cliente.nome, mes;




# Indicadores de Desempenho


| Indicador                       | Objetivo                                       | Descrição                                                                                         | Fórmula de cálculo                        | Fontes de dados  | Perspectiva     |
|---------------------------------|------------------------------------------------|---------------------------------------------------------------------------------------------------|-------------------------------------------|------------------|-----------------|
| Taxa de utilização de Frota      | Avaliar quantitativamente o número de veículos utilizados | Percentual de veículos alugados | (número de veículos alugados / número de veículos da frota) * 100 | Tabela de veículos | Crescimento     |
| Receita em taxas extras          | Avaliar a receita obtida secundariamente ao aluguel | Mede a receita total obtida somente pelas taxas extras, sendo elas devido a quebras de contrato, estado do veículo, etc. | (receita total em taxas / receita total) * 100 | Tabela de aluguel | Crescimento     |
| Receita por Veículo Alugado      | Avaliar o lucro obtido no total por veículo     | Receita total por veículo alugado | receita total / número de veículos alugados                     | Tabela de aluguel | Aprendizado     |
| Taxa de Manutenção               | Medir o percentual de veículos que estiveram em manutenção | % de veículos que em algum momento estiveram em manutenção em relação à toda a frota       | (veículos que estiveram em manutenção / total de veículos da frota) * 100 | Tabela de veículos | Redução         |
| Taxa de Retorno de Cliente       | Avaliar clientes que utilizam o serviço        | % de clientes que retornam a utilizar o serviço                                                    | (número de Clientes Ativos / número Total de Clientes) * 100 | Tabela de aluguel e de clientes | Crescimento     |


-----------------------------------------------------------------------------

