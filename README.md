# Traffic-Fines-Extraction

Consulta Cidadão ETL
Descrição
Este projeto contém um script Python que realiza um processo ETL (Extract, Transform, Load) para extrair informações de infrações de trânsito de múltiplos sites do sistema Consulta Cidadão (ex.: Diadema, São Caetano do Sul, Mauá, etc.). O script faz login nos sites, extrai dados como placas, autos de infração, datas e status, e salva tudo em um arquivo CSV consolidado.
Funcionalidades

Extração: Acessa sites do Consulta Cidadão, faz login e extrai informações de infrações associadas às placas registradas.
Transformação: Estrutura os dados extraídos em um formato tabular, tratando casos em que não há infrações.
Carregamento: Salva os dados em um arquivo CSV (infracoes.csv) com colunas para Site, Placa, Auto de Infração, Data da Infração e Status.

Tecnologias Utilizadas

Python 3.8+
Bibliotecas:
undetected-chromedriver: Para automação de navegador com Chrome, contornando detecções anti-bot.
selenium: Para interagir com elementos dinâmicos das páginas web.
beautifulsoup4: Para parsing de HTML e extração de dados.
csv: Para manipulação e exportação de dados em formato CSV.



Pré-requisitos

Python 3.8 ou superior instalado.
Google Chrome instalado (versão compatível com undetected-chromedriver).
Credenciais válidas (login e senha) para os sites do Consulta Cidadão.


Este script é um exemplo clássico de um processo ETL (Extract, Transform, Load), que pode ser dividido em três etapas principais:

Extração (Extract): O script utiliza undetected-chromedriver e selenium para acessar os sites do Consulta Cidadão, realizar login automático e extrair informações de infrações de trânsito (placas, autos de infração, datas e status). A biblioteca beautifulsoup4 é usada para parsear o HTML e localizar os elementos relevantes na página.

Transformação (Transform): Os dados extraídos são estruturados em um formato tabular (dicionário Python) e tratados para lidar com casos em que não há infrações (ex.: preenchendo com "Nenhum" ou "Nenhuma" quando aplicável). A lógica também associa corretamente autos de infração com suas respectivas datas e status, mesmo em estruturas HTML complexas.

Carregamento (Load): Os dados processados são salvos em um arquivo CSV (infracoes.csv) com colunas bem definidas: Site, Placa, Auto de Infração, Data da Infração e Status.


Estrutura do Script

Configuração inicial: Define as credenciais de login e uma lista de sites a serem processados, com URLs e nomes amigáveis (ex.: Diadema, São Caetano).
Função processar_site:
Abre o site no Chrome com undetected-chromedriver.
Fecha pop-ups iniciais, se presentes.
Navega até a seção "Indicação de Condutor".
Realiza login com as credenciais fornecidas.
Rola a página para carregar todo o conteúdo dinâmico.
Extrai e organiza os dados de infrações.


Saída: Gera um arquivo CSV consolidado com os dados de todos os sites processados.

Exemplo de Saída
O arquivo infracoes.csv gerado tem a seguinte estrutura:

Site,Placa,Auto de Infração,Data da Infração,Status
Diadema,ABC1234,123456789,01/01/2023,Indicação Protocolada
Sao Caetano,XYZ5678,Nenhum,Nenhuma,Indicação Liberada Data limite:xx/xx/xxxx
Maua,DEF9012,987654321,15/02/2023,Indicação Condutor com Pendência

Configuração

Credenciais: Edite as variáveis LOGIN e SENHA no script com suas credenciais válidas.
Lista de Sites: A variável SITES contém os URLs e nomes dos sites a processar. Para adicionar ou remover sites, edite o dicionário SITES (ex.: descomente as linhas de Mogi das Cruzes ou Caieiras, se necessário).
Timeouts: O script usa WebDriverWait para aguardar o carregamento de elementos dinâmicos. Ajuste os tempos de espera (em segundos) se necessário para sites mais lentos.

Limitações

Dependência da Estrutura HTML: O script depende da estrutura HTML dos sites do Consulta Cidadão. Alterações no layout ou classes CSS podem exigir ajustes no código.
Credenciais: Credenciais válidas são obrigatórias. Credenciais incorretas causarão falhas no login.
Detecção Anti-bot: Embora o undetected-chromedriver contorne algumas detecções, sites com proteção avançada podem bloquear o acesso.
Conexão com a Internet: Uma conexão estável é necessária para evitar falhas durante a extração.
Performance: O script processa os sites sequencialmente. Para grandes quantidades de sites, considere implementar paralelização.

