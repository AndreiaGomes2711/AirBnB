# AirBnB
A análise visou identificar oportunidades estratégicas para otimização da performance na plataforma Airbnb, utilizando dados de listagens, anfitriões e reservas, com foco em eficiência de receita, comportamento de demanda e desempenho geográfico.

Plataforma: Airbnb (ou similar)
Ferramentas: Power BI | BigQuery
Linguagens: SQL (BigQuery) + DAX (Power BI)
✅ 1. Resumo Executivo
Este projeto de BI tem como objetivo construir um painel dinâmico e estratégico com foco em propriedades de aluguel de temporada. Ele oferece uma visão analítica completa sobre desempenho, engajamento e rentabilidade, apoiando tanto anfitriões quanto a gestão da plataforma em ações orientadas por dados.

Resultados esperados:

Compreensão clara dos padrões de reservas.

Identificação de sazonalidades, oportunidades de precificação e saturação de mercado.

Monitoramento de KPIs críticos, permitindo tomada de decisão com base em dados reais.

🎯 2. Objetivos do Projeto
Identificar regiões mais lucrativas (ocupação x receita).

Avaliar relação entre tipo de imóvel, preço e demanda.

Medir performance dos anfitriões.

Detectar sazonalidades e padrões de reserva.

Monitorar KPIs como ADR, RevPAR, disponibilidade e receita.

Propor estratégias de precificação dinâmica baseada em dados históricos.

📦 3. Escopo
Incluído:

Análise de propriedades, preços, reviews e localização.

KPIs de performance, engajamento e ocupação.

Dashboards interativos Power BI.

Excluído (futuro):

Machine Learning (previsão de preços).

Integrações via API externas em tempo real.

🔗 4. Fontes de Dados
1. rooms (Dimensão):
Dados de imóveis – localização, tipo, mínimo de noites.

2. hosts (Dimensão):
Identificação e nome do anfitrião.

3. reviews (Fato):
Preço, número de reviews, datas, disponibilidade e listagens por host.

🧱 5. Modelagem de Dados
Modelo Estrela:

Fato: reviews_cleaned

Dimensões: rooms_cleaned_v3, hosts_cleaned, dim_tempo

Relacionamentos:

rooms 1:* reviews (via id)

hosts 1:* reviews (via host_id)

🧰 6. ETL e Preparação de Dados (BigQuery)
Limpeza e tratamento:

Exclusão de nulos e duplicados com lógica ROW_NUMBER().

Correção de colunas trocadas (ex: id vs name, longitude vs room_type).

Criação de colunas derivadas: last_review_corrigido, number_of_reviews_corrigido.

Validação de dados anômalos via expressões regulares e SAFE_CAST.

Exemplo de Métricas criadas via SQL e DAX:


Revenue Potencial = [availability_365] * [price]
Revenue Real Estimado = [price] * [reviews_per_month] * 12
Revenue Não Explorado = [Revenue Potencial] - [Revenue Real Estimado]
📊 7. Principais Dashboards Criados
📍 1. Receita & Ocupação
Revenue total por região.

Mapa de calor (latitude/longitude).

Preço médio e disponibilidade média por bairro.

🏠 2. Tipo de Imóvel vs Preço vs Demanda
Preço médio por tipo (Entire home/apt, Private room, etc.).

Total de receita e engajamento por tipo.

👤 3. Anfitriões Relevantes
Receita e reviews por host.

Contagem de imóveis por host (identifica concentração).

📅 4. Sazonalidade e Padrões de Reserva
Evolução de reviews ao longo do tempo.

Comparativo por bairro e tipo de imóvel.

🚨 5. Potencial de Receita Não Explorado
Revenue Potencial x Real x Não Explorado.

Mapa com bolhas por região.

Gráficos de dispersão com availability_365 e reviews_per_month.

📌 8. KPIs Criados
Nome	Fórmula
Revenue Potencial	availability_365 * price
Revenue Real Estimado	reviews_per_month * price * 12
Revenue Não Explorado	Revenue Potencial - Revenue Real
% Potencial Aproveitado	Revenue Real / Revenue Potencial
Reviews por Mês (Proxy)	Representa engajamento ≈ demanda real
Preço Médio por Tipo	Média price por room_type
Disponibilidade Média	Média de availability_365 por região
Contagem de imóveis por host	Distinct Count de id agrupado por host_id ou nome do host

🔍 9. Proxy de Demanda: reviews_per_month
Como não há dados de reservas reais, utilizamos reviews_per_month como proxy para estimar demanda e receita. Assumimos que cada review representa uma fração das reservas.

📈 10. Principais Insights do Projeto
Manhattan concentra as maiores receitas, preços e engajamento.

Brooklyn tem bom volume de imóveis, mas menor receita média.

Staten Island e Bronx possuem alta disponibilidade, mas baixa demanda → potencial não explorado.

"Entire home/apt" tem maior preço, porém não garante maior demanda.

Hosts concentradores: pequeno grupo controla grande parte das listagens e receita.

Sazonalidade clara: picos de reviews em meados do ano.

Revenue Não Explorado alto em regiões periféricas → oportunidade de campanha/promoção.

Uso de mapa com bolhas e gráficos de dispersão facilitam a leitura visual dos extremos.

✅ 11. Recomendações Estratégicas
Aplicar precificação dinâmica em imóveis com baixo aproveitamento de potencial.

Incentivar hosts subutilizados com sugestões baseadas em dados.

Foco em expansão estratégica em bairros com alta disponibilidade e demanda reprimida.

Campanhas regionais para Bronx, Queens e Staten Island.

Revisar políticas de tipo de imóvel por região conforme engajamento.

Links do projeto

## Documentacao tecnica

https://www.notion.so/Documentacao-Tecnica-2171f093899980e4a0d5ccfa69fe8b2e?source=copy_link

## Big Query

https://console.cloud.google.com/bigquery?hl=pt&invt=Ab2S1w&project=airbnbbi&inv=1&ws=!1m10!1m4!4m3!1sairbnbbi!2sDataset!3sreviews_cleaned_v2!1m4!4m3!1sairbnbbi!2sDataset!3sDias_ultima_review!1m5!1m4!1m3!1sairbnbbi!2sbquxjob_190f537b_197efb4af3d!3sUS

## Power Bi

https://app.powerbi.com/groups/me/reports/fd53ee24-2861-4705-93dc-f10a922ab252/0681160a30ea8281c003?bookmarkGuid=c95f039f-1a61-4fb3-9d60-9e097ee2166f&bookmarkUsage=1&ctid=042262d3-8402-4888-9226-87f5d16a9209&portalSessionId=d35413a8-7331-4c11-88d1-33108e17cf3b&fromEntryPoint=export

## Apresentacao

https://docs.google.com/presentation/d/1BgpLKsJdJc6wTOQlcLerFKgcKo7ZE5lwNigmvHgkvmw/edit?usp=sharing

## Video

https://www.loom.com/share/96324639eb7047a28dd0e9419e62200b?sid=458d64e5-239a-441b-bd33-9aa25d05bc23
