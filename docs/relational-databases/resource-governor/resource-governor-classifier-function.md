---
title: Função do classificador do Resource Governor | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: resource-governor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, classifier function
- user-defined functions [SQL Server], classifier function
- classifier function [SQL Server]
- classifier function [SQL Server], overview
ms.assetid: 64c25012-7068-476f-afa2-0b4f3adde9a4
caps.latest.revision: 7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e6b9e3973524537811d8827ec7e670ed513be665
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="resource-governor-classifier-function"></a>Função de classificação do Administrador de Recursos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O processo de classificação do administrador de recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atribui sessões de entrada a um grupo de cargas de trabalho baseado nas características da sessão. Você pode personalizar a lógica de classificação gravando uma função definida pelo usuário, chamado de função de classificador.  
  
## <a name="classification"></a>Classificação  
 O Administrador de Recursos oferece suporte à classificação de sessões de entrada. A classificação baseia-se em um conjunto de critérios gravados pelo usuário contido em uma função. Os resultados da lógica de função permitem que o Administrador de Recursos classifique as sessões em grupos de carga de trabalho existentes.  
  
> [!NOTE]  
>  O grupo de carga de trabalho interno é populado com solicitações que são apenas para uso interno. Você não pode alterar os critérios usados para direcionar essas solicitações nem classificar as solicitações no grupo de carga de trabalho interno.  
  
 É possível gravar uma função escalar contendo a lógica que é usada para atribuir sessões de entrada a um grupo de carga de trabalho. Para que você possa usar essa função, é necessário concluir as seguintes ações:  
  
-   Crie e registre a função usando a instrução ALTER RESOURCE GOVERNOR. Para obter mais informações, veja [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md).  
  
-   Atualize a configuração do Administrador de Recursos usando a instrução ALTER RESOURCE GOVERNOR com o parâmetro RECONFIGURE.  
  
 Depois que você criar a função e aplicar as alterações de configuração, o classificador do Administrador de Recursos usará o nome do grupo de carga de trabalho retornado pela função para enviar uma nova solicitação ao grupo de carga de trabalho adequado.  
  
> [!IMPORTANT]  
>  A sessão do cliente pode expirar caso a função de classificação não seja concluída dentro do tempo limite especificado para o logon. Tempo limite de logon é uma propriedade do cliente e, como tal, o servidor desconhece o tempo limite. Uma função de classificação com execução longa pode deixar o servidor com conexões órfãs por períodos longos. É importante que se criem funções de classificação que terminem de executar antes do tempo limite de conexão.  
  
 A função definida pelo usuário tem as seguintes características e comportamentos:  
  
-   A função definida pelo usuário é avaliada para cada sessão nova, mesmo quando o pooling de conexões está habilitado.  
  
-   A função definida pelo usuário fornece contexto de grupo de carga de trabalho para a sessão. Depois que a associação em grupo é determinada, a sessão é associada ao grupo de carga de trabalho durante o tempo de vida da sessão.  
  
-   Se a função definida pelo usuário retornar NULL, padrão ou o nome de um grupo inexistente, o contexto de grupo de carga de trabalho padrão será dado à sessão. O contexto padrão também será dado à sessão caso a função falhe por qualquer motivo.  
  
-   A função deve ser definida com escopo do servidor (banco de dados mestre).  
  
-   A designação de função de classificação definida pelo usuário só entrará em vigor depois que ALTER RESOURCE GOVERNOR RECONFIGURE for executada.  
  
-   Só uma função definida pelo usuário pode ser designada como classificação por vez.  
  
-   A função de classificação definida pelo usuário não pode ser descartada ou alterada a menos que seu estado de classificação seja removido.  
  
-   Na ausência de uma função de classificação definida pelo usuário, todas as sessões são classificadas no grupo padrão.  
  
-   O grupo de carga de trabalho retornado pela função de classificação está fora do escopo da restrição de associação de esquema. Por exemplo, você não pode descartar uma tabela, mas pode descartar um grupo de cargas de trabalho.  
  
> [!IMPORTANT]  
>  É recomendável habilitar a conexão de administrador dedicada (DAC) no servidor. A DAC não está sujeita à classificação do Administrador de Recursos e pode ser usada para monitorar e solucionar problemas de uma função de classificação. Para obter mais informações, veja [Conexão de diagnóstico para administradores de banco de dados](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md). Se uma DAC não estiver disponível para a solução de problemas, a outra opção é reiniciar o sistema no modo de usuário único. Embora o modo de usuário único não esteja sujeito a classificação, ele não oferece a você a capacidade de diagnosticar a classificação do Administrador de Recursos enquanto está em execução.  
  
### <a name="classification-process"></a>Processo de classificação  
 No contexto do Administrador de Recursos, o processo de logon para uma sessão consiste nas seguintes etapas:  
  
1.  Autenticação de logon  
  
2.  Execução de gatilhos LOGON  
  
3.  Classificação  
  
 Quando a classificação é iniciada, o Administrador de Recursos executa a função de classificação e usa o valor retornado pela função para enviar solicitações ao grupo de cargas de trabalho apropriado.  
  
> [!NOTE]  
>  As informações sobre a execução da função de classificação e dos gatilhos LOGON são expostas em [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md) e [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).  
  
## <a name="classification-function-tasks"></a>Tarefas da função de classificação  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Descreve como criar e testar uma função de classificação definida pelo usuário.|[Criar e testar uma função de classificação definida pelo usuário](../../relational-databases/resource-governor/create-and-test-a-classifier-user-defined-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Administrador de Recursos](../../relational-databases/resource-governor/resource-governor.md)   
 [Habilitar Administrador de Recursos](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [Pool de recursos do Administrador de Recursos](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [Grupos de carga de trabalho do Administrador de Recursos](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [Configurar o administrador de recursos usando um modelo](../../relational-databases/resource-governor/configure-resource-governor-using-a-template.md)   
 [Exibir Propriedades do Administrador de Recursos](../../relational-databases/resource-governor/view-resource-governor-properties.md)  
  
  
