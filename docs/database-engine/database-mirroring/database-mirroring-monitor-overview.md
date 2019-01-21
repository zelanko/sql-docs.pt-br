---
title: Visão geral do Monitor de Espelhamento de Banco de Dados | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.dbmmonitor.main.f1
helpviewer_keywords:
- Database Mirroring Monitor [SQL Server], interface
ms.assetid: 8ebbdcd6-565a-498f-b674-289c84b985eb
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e25084fc5c472021b3159204116a04d1c3fb0174
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54126346"
---
# <a name="database-mirroring-monitor-overview"></a>Visão geral do Monitor de Espelhamento de Banco de Dados
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Se tiver as permissões corretas, você pode usar o Monitor de Espelhamento de Banco de Dados para monitorar qualquer subconjunto de bancos de dados espelhado em uma instância de servidor. O monitoramento permite verificar como e se os dados estão fluindo satisfatoriamente na sessão de espelhamento de banco de dados. O Monitor de Espelhamento de Banco de Dados é também útil para solucionar problemas da causa da redução do fluxo de dados.  
  
 Você pode registrar qualquer um dos bancos de dados espelhados para monitoramento em cada um dos parceiros de failover individualmente. Quando você registra um banco de dados, o Monitor de Espelhamento de Banco de Dados armazenará em cache as seguintes informações do banco de dados.  
  
-   Nome do banco de dados  
  
-   Os nomes de ambas as instâncias do servidor parceiro.  
  
-   As últimas funções conhecidas de cada parceiro (principal ou espelho)  
  
## <a name="permissions"></a>Permissões  
 Para monitorar o espelhamento de banco de dados é necessário ser um membro da função de servidor fixa **sysadmin** ou da função de banco de dados fixa **dbm_monitor** no banco de dados **msdb** na instância do servidor. Se você for um membro do **sysadmin** ou do **dbm_monitor** em apenas uma das instâncias do servidor parceiro, o monitor poderá se conectar apenas àquele parceiro e não poderá recuperar as informações do outro parceiro.  
  
 Se você for um membro de **dbm_monitor** em apenas uma instância de servidor, terá permissões limitadas naquela instância de servidor. Você só poderá visualizar a linha de status mais recente. Se você se conectar a uma instância de servidor usando as permissões do **dbm_monitor** em uma instância de servidor, o Monitor de Espelhamento de Banco de Dados vai informá-lo de que suas permissões são limitadas.  
  
> [!IMPORTANT]  
>  A função fixa **dbm_monitor** do banco de dados é criada no banco de dados **msdb** quando o primeiro banco de dados for registrado no Monitor de Espelhamento de Banco de Dados. A nova função **dbm_monitor** não tem nenhum membro até que um administrador de sistemas atribua usuários à função.  
  
## <a name="navigation-tree"></a>Árvore de navegação  
 Se algum banco de dados for registrado para monitoramento pelo Monitor de Espalhamento de Banco de Dados, uma lista dos bancos de dados registrados será exibida na árvore de navegação. A árvore é atualizada automaticamente a cada 30 segundos. Para ver o status de um banco de dados registrado, selecione-o. Para obter mais informações, consulte "Painel de Detalhes” mais adiante neste tópico.  
  
 Para cada banco de dados registrado, as seguintes informações serão exibidas:  
  
 _<Database_name>_ **(** _\<Status>_ **,** _<PRINCIPAL_SERVER>_ **->** _<MIRROR_SERVER>_ **)**  
  
 *<nome_do_banco_de_dados>*  
 O nome de um banco de dados espelho registrado no Monitor de Espelhamento de Banco de Dados.  
  
 *\<Status>*  
 Os possíveis status e seus ícones associados são os seguintes:  
  
|Ícone|Status|Descrição|  
|----------|------------|-----------------|  
|Ícone de aviso:|**Desconhecido**|O monitor não está conectado a nenhum parceiro. As únicas informações disponíveis são aquelas armazenadas em cache pelo monitor.|  
|Ícone de aviso:|**Sincronizando**|O conteúdo do banco de dados espelho está ficando atrás do conteúdo do banco de dados principal. A instância do servidor principal está enviando registros de log para a instância do servidor espelho, a qual está aplicando as alterações ao banco de dados espelho para rolagem para frente.<br /><br /> No início de uma sessão de espelhamento de banco de dados, o banco de dados espelho e principal estão nesse estado.|  
|Cilindro padrão do banco de dados|**Sincronizado**|Quando o servidor espelho torna-se suficientemente atualizado em relação ao servidor principal, o estado do banco de dados é alterado para **Sincronizado**. O banco de dados permanece nesse estado enquanto o servidor principal continua enviando alterações para o servidor espelho e o servidor espelho continua aplicando as alterações ao banco de dados espelho.<br /><br /> Para o modo de alta segurança, o failover automático e o failover manual são ambos possíveis, sem perda de dados.<br /><br /> No modo de alto desempenho, alguma perda de dados é sempre possível, mesmo no estado **Sincronizado** .|  
|Ícone de aviso:|**Suspenso**|O banco de dados principal está disponível, mas não está enviando logs para o servidor espelho.|  
|Ícone de erro|**Desconectado**|A instância do servidor não pode se conectar ao seu parceiro.|  
  
 *<SERVIDOR_PRINCIPAL>*  
 O nome do parceiro que atualmente é a principal instância do servidor. O nome está no seguinte formato:  
  
 *<SYSTEM_NAME>*[**\\**_<instance_name>_]  
  
 em que *<SYSTEM_NAME>* é o nome do sistema no qual a instância do servidor reside. Para uma instância de servidor não padrão, o nome da instância também é exibido: _<SYSTEM_NAME>_**\\**_<instance_name>_.  
  
 *<SERVIDOR_ESPELHO>*  
 O nome do parceiro que é atualmente a instância do servidor espelho. O formato é o mesmo do servidor principal.  
  
## <a name="detail-pane"></a>Painel de detalhes  
 A aparência do monitor depende se um banco de dados foi selecionado ou não. Quando você abre o monitor, o painel de detalhes exibe um link **Registrar Banco de Dados Espelho** . Clique nele para registrar um banco de dados. Os bancos de dados registrados estão listados abaixo do nó **Monitor de Espelhamento de Banco de Dados** na árvore de navegação. O Monitor de Espelhamento de Banco de dados tenta sempre se conectar a cada instância do servidor para a qual ele tem credenciais armazenadas.  
  
 Quando você selecionar um banco de dados, seu status é exibido na página com guias **Status** no painel de detalhes. O conteúdo desta página vem das duas instâncias de servidor principal e espelho. A página é preenchida de forma assíncrona conforme o status é coletado através de conexões separadas às instâncias de servidor principal e espelho. O status é atualizado automaticamente em intervalos de 30 segundos.  
  
> [!NOTE]  
>  Não é possível alterar a taxa de atualização do monitor, mas pode atualizar a tabela de status por meio da caixa de diálogo **Histórico do Espelhamento de Banco de Dados** .  
  
 O administrador de sistemas pode visualizar a configuração de avisos atual do banco de dados, selecionando a página com guias **Avisos** . A partir deste ponto, o administrador pode iniciar a caixa de diálogo **Definir Limites de Aviso** para habilitar e configurar um ou mais limites de aviso.  
  
 Na faixa acima das guias, o painel de detalhes exibe a última vez em que o monitor atualizou as informações de status, como **Última atualização**_\<date>\<time>_. Geralmente, o Monitor de Espelhamento de Banco de Dados recupera as informações de status a partir das instâncias de servidor principal e espelho em horários diferentes. O horário mais antigo dessas duas atualizações é exibido.  
  
## <a name="action-menu"></a>Menu Ação  
 O menu **Ação** contém sempre os seguintes comandos:  
  
|Comando|Descrição|  
|-------------|-----------------|  
|**Registrar um Banco de Dados Espelho**|Abre a caixa de diálogo **Registrar Banco de Dados Espelho** . Use esta caixa de diálogo para registrar um ou mais bancos de dado espelhados em uma determinada instância do servidor, adicionando o banco de dados, ou bancos de dados, ao Monitor de Espelhamento de Banco de Dados. Quando um banco de dados é adicionado, o Monitor de Espelhamento de Banco de Dados armazena localmente em cache as informações do banco de dados, seus parceiros e como se conectar aos parceiros.|  
|**Gerenciar Conexões das Instâncias do Servidor...**|Quando você seleciona este comando, a caixa de diálogo **Gerenciar Conexões do Servidor** é exibida. Nela, você pode escolher uma instância de servidor para a qual deseja especificar as credencias a serem usadas pelo monitor quando se conectar a um determinado parceiro de failover.<br /><br /> Para editar as credenciais para o parceiro, localize sua entrada na grade **Instância de servidor** , e clique em **Editar** naquela linha. Isto exibe a caixa de diálogo **Conectar ao Servidor** com o nome de instância de servidor e com os controles de credenciais inicializados com o valor atual em cache. Altere as informações de autenticação conforme necessário e clique em **Conectar**. Se as credenciais tiverem privilégios suficientes, a coluna **Conectar Usando** é atualizada com as novas credenciais.|  
  
 Se você selecionar o banco de dados, o menu **Ação** também conterá os seguintes comandos:  
  
|Comando|Descrição|  
|-------------|-----------------|  
|**Cancelar o Registro deste Banco de Dados.**|Remove o banco de dados selecionado do Monitor de Espelhamento de Banco de Dados.|  
|**Definir Limites de Aviso...**|Abre a caixa de diálogo **Definir Limites de Aviso** . A partir deste ponto, o administrador pode habilitar ou desabilitar os avisos para o banco de dados em cada um dos parceiros e alterar o limite de cada aviso. Recomendamos definir o limite de um determinado aviso em ambos os parceiros a fim de garantir que o aviso continue se houver um failover no banco de dados. O limite adequado para cada parceiro depende das capacidades de desempenho o sistema daquele parceiro.<br /><br /> Um evento de desempenho é gravado no log de eventos somente se o seu valor estiver no seu limite ou acima dele quando a tabela de status for atualizada. Se um valor máximo alcançar temporariamente o limite entre as atualizações de status, este valor máximo é ignorado|  
  
 **Para monitorar o espelhamento de banco de dados usando o SQL Server Management Studio para**  
  
-   [Iniciar o Monitor de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorando o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [Iniciar o Assistente para Configurar Segurança de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)  
  
  
