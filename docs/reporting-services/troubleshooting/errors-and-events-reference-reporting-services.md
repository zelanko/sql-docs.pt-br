---
title: Referência de erros e eventos (Reporting Services) | Microsoft Docs
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 04/26/2019
ms.openlocfilehash: 21daadd4301444b75f80961949396741f0ad04e8
ms.sourcegitcommit: 1800fc15075bb17b50d0c18b089d8a64d87ae726
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2019
ms.locfileid: "66500216"
---
# <a name="errors-and-events-reference-reporting-services"></a>Referência de erros e eventos (Reporting Services)

Este tópico fornece informações sobre erros e eventos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Os arquivos de log do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] também contêm informações de erro. Para obter mais informações sobre os tipos de arquivos de log que estão disponíveis e como exibir os logs, consulte [Fontes e arquivos de log do Reporting Services](../../reporting-services/report-server/reporting-services-log-files-and-sources.md).  

## <a name="cause-and-resolution-for-reporting-services-error-messages"></a>Causa e resolução de mensagens de erro do Reporting Services  

Causa e informações de resolução estão disponíveis para os erros mais frequentemente procurados nos sites da Web da [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Para obter informações, consulte [Causa e resolução de erros do Reporting Services](../../reporting-services/troubleshooting/cause-and-resolution-of-reporting-services-errors.md).  
  
## <a name="report-server-events"></a>Eventos do servidor de relatório

Os eventos a seguir do servidor de relatório são registrados no log do aplicativo do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
|ID do evento|Tipo|Categoria|Origem|Descrição|  
|--------------|----------|--------------|------------|-----------------|  
|106|Erro|Agendamento|Servidor de relatório|O SQL Server Agent deve estar em execução quando você define uma operação agendada (por exemplo, assinatura e entrega de relatório).|  
|[107](../../reporting-services/troubleshooting/report-server-windows-service-mssqlserver-107.md)|Erro|Inicialização/desligamento|Servidor de relatório<br /><br /> Processador de agendamento e entrega|A *\<Source>* não pode se conectar ao banco de dados do servidor de relatório. Para obter mais informações, consulte [Serviço Windows do Servidor de Relatório &#40;MSSQLServer&#41; 107](../../reporting-services/troubleshooting/report-server-windows-service-mssqlserver-107.md).|  
|108|Erro|Extensão|Servidor de relatório<br /><br /> Gerenciador de Relatórios|A *\<Source>* não pode carregar uma extensão de entrega, de processamento de dados ou de renderização.<br /><br /> Provavelmente, esse é o resultado de uma implantação incompleta ou remoção de uma extensão. Para obter mais informações, consulte [Implantando uma extensão de processamento de dados](../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md) e [Implantando uma extensão de entrega](../../reporting-services/extensions/delivery-extension/deploying-a-delivery-extension.md).|  
|109|Informações|Gerenciamento|Servidor de relatório<br /><br /> Gerenciador de Relatórios|Um arquivo de configuração foi modificado. Para saber mais, confira [Arquivos de Configuração do Reporting Services](../../reporting-services/report-server/reporting-services-configuration-files.md).|  
|110|Aviso|Gerenciamento|Servidor de relatório<br /><br /> Gerenciador de Relatórios|Uma configuração em um dos arquivos de configuração foi modificada e não é mais válida. Um valor padrão será usado em vez disso. Para saber mais, confira [Arquivos de Configuração do Reporting Services](../../reporting-services/report-server/reporting-services-configuration-files.md).|  
|111|Erro|Log|Servidor de relatório<br /><br /> Gerenciador de Relatórios|A *\<Source>* não pode criar o log de rastreamento. Para obter mais informações, consulte [Report Server Service Trace Log](../../reporting-services/report-server/report-server-service-trace-log.md).|  
|112|Aviso|Segurança|Servidor de relatório|O servidor de relatório detectou uma possível negação de ataque de serviço. Para obter mais informações, consulte [Segurança e proteção do Reporting Services](../../reporting-services/security/reporting-services-security-and-protection.md).|  
|113|Erro|Log|Servidor de relatório|O servidor de relatório não pode criar um contador de desempenho.|  
|114|Erro|Inicialização/desligamento|Gerenciador de Relatórios|O Gerenciador de Relatórios não pode se conectar ao serviço Servidor de Relatório.|  
|115|Aviso|Agendamento|Processador de agendamento e entrega|Uma tarefa agendada na fila do SQL Server Agent foi modificada ou excluída.|  
|116|Erro|Internal|Servidor de relatório<br /><br /> Gerenciador de Relatórios<br /><br /> Processador de agendamento e entrega|Ocorreu um erro interno.|  
|117|Erro|Inicialização/desligamento|Servidor de relatório|O banco de dados do servidor de relatório é uma versão inválida.|  
|118|Aviso|Log|Servidor de relatório<br /><br /> Gerenciador de Relatórios|O arquivo de rastreamento não está mais no local do diretório previsto; um novo arquivo de rastreamento será criado no diretório padrão. Para obter mais informações, consulte [Report Server Service Trace Log](../../reporting-services/report-server/report-server-service-trace-log.md).|  
|119|Erro|Ativação|Servidor de relatório<br /><br /> Processador de agendamento e entrega|A *\<Source>* não recebeu acesso ao conteúdo do banco de dados do servidor de relatório.|  
|120|Erro|Ativação|Servidor de relatório|A chave simétrica não pode ser descriptografada. Provavelmente, houve uma alteração na conta na qual o serviço é executado. Para obter mais informações, consulte [Configurar e gerenciar chaves de criptografia &#40;Gerenciador de Configurações do SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md).|  
|121|Erro|Inicialização/desligamento|Servidor de relatório|Falha ao iniciar o serviço RPC (Chamada de Procedimento Remoto).|  
|122|Aviso|Entrega|Processador de agendamento e entrega|O Processador de Agendamento e Entrega não pode se conectar ao servidor de SMTP usado para entrega de email. Para obter mais informações sobre conexões de servidor SMTP, consulte [configurações de email – modo nativo do Reporting Services (Configuration Manager)](../install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md).|  
|123|Aviso|Log|Servidor de relatório<br /><br /> Gerenciador de Relatórios|Falha no servidor de relatório ao gravar o log de rastreamento. Para obter mais informações sobre logs de rastreamento, consulte [Log de rastreamento do serviço Servidor de Relatório](../../reporting-services/report-server/report-server-service-trace-log.md).|  
|124|Informações|Ativação|Servidor de relatório|O serviço Servidor de Relatório foi iniciado. Para obter mais informações, consulte [Inicializar um Servidor de Relatório &#40;Gerenciador de Configurações do SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md).|  
|125|Informações|Ativação|Servidor de relatório|A chave usada para criptografar dados foi extraída com êxito. Para obter mais informações sobre chaves, consulte [Configurar e gerenciar chaves de criptografia &#40;Gerenciador de Configurações do SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md).|  
|126|Informações|Ativação|Servidor de relatório|A chave usada para criptografar dados foi aplicada com êxito. Para obter mais informações sobre chaves, consulte [Configurar e gerenciar chaves de criptografia &#40;Gerenciador de Configurações do SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md).|  
|127|Informações|Ativação|Servidor de relatório|O conteúdo criptografado foi removido com êxito do banco de dados do servidor de relatório. Para obter mais informações sobre como excluir dados criptografados não recuperáveis, consulte [Configurar e gerenciar chaves de criptografia &#40;Gerenciador de Configurações do SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md).|  
|128|Erro|Ativação|Servidor de relatório|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Componentes de edições diferentes não podem ser usados juntos.|  
|129|Erro|Gerenciamento|Servidor de relatório<br /><br /> Processador de agendamento e entrega|Uma definição de arquivo de configuração criptografada não pode ser descriptografada.|  
|130|Erro|Gerenciamento|Servidor de relatório<br /><br /> Processador de agendamento e entrega|A *\<Source>* não pode localizar o arquivo de configuração. Arquivos de configuração são exigidos pelo servidor de relatório.|  
|131|Erro|Segurança|Servidor de relatório<br /><br /> Processador de agendamento e entrega|Um valor de dados de usuário criptografado não pôde ser descriptografado.|  
|132|Erro|Segurança|Servidor de relatório|Ocorreu uma falha durante a criptografia de dados de usuário. O valor não pode ser salvo.|  
|133|Erro|Gerenciamento|Servidor de relatório<br /><br /> Gerenciador de Relatórios<br /><br /> Processador de agendamento e entrega|Falha no carregamento da configuração do arquivo. Esse erro poderá ocorrer se o XML não for válido.|  
|134|Erro|Gerenciamento|Servidor de relatório|Falha no servidor de relatório ao criptografar valores para uma configuração em um arquivo de configuração.|  
  
## <a name="see-also"></a>Confira também

- [Monitorar assinaturas do Reporting Services](../../reporting-services/subscriptions/monitor-reporting-services-subscriptions.md)
- [Fontes e arquivos de log do Reporting Services](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)
