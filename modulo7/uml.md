# Jornada do Usuário

Um usuário deseja acessar sua fatura da Vivo através de um aplicativo móvel. Ele abre o aplicativo, faz login e solicita o acesso à sua fatura. O sistema então inicia o processo de busca pelos dados da fatura, que envolve comunicação com os três microserviços: telefonia, internet e outros, através do barramento. O barramento também se comunica com a API de fatura para obter informações adicionais. Durante esse processo, o sistema verifica se os dados estão disponíveis no sistema de cache para otimizar o tempo de resposta. Após a obtenção dos dados necessários, o sistema retorna a fatura para o usuário no aplicativo.

# Diagrama de Sequência

```plantuml
@startuml
participant Usuario
participant Aplicativo
participant Sistema
participant Barramento
participant MicroservicoTelefonia
participant MicroservicoInternet
participant MicroservicoOutros
participant APIFatura
participant SistemaDeCache

Usuario -> Aplicativo: Fazer login
Aplicativo -> Sistema: Solicitar fatura
Sistema -> Barramento: Enviar requisição de fatura
Barramento -> SistemaDeCache: Verificar disponibilidade de dados em cache
Barramento -> MicroservicoTelefonia: Buscar dados dad telefonia
Barramento -> MicroservicoInternet: Buscar dados da internet
Barramento -> MicroservicoOutros: Buscar outros dados
Barramento -> APIFatura: Consultar dados adicionais da fatura
Barramento -> Sistema: Retornar dados da fatura
Sistema -> Aplicativo: Enviar fatura para exibição
@enduml
