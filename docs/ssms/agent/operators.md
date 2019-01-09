---
title: Operadores | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- operators (users) [Database Engine]
- fail-safe operator [SQL Server]
- aliases [SQL Server], operators
- SQL Server Agent alerts, operators
- contact information [SQL Server Agent]
- net send [SQL Server]
- e-mail [SQL Server], SQL Server Agent operators
- pager notifications [SQL Server Agent]
- mail [SQL Server], SQL Server Agent operators
- operators (users) [Database Engine], defining
- jobs [SQL Server Agent], operators
- alerts [SQL Server], operators
ms.assetid: 38e8488f-2669-4cea-b9c3-5f394a663678
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 60e05754e43056e3f71d4abccb1d8af91c650684
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53212115"
---
# <a name="operators"></a>Operadores
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Operadores são aliases de pessoas ou grupos que podem receber notificações eletrônicas sobre a conclusão de trabalhos ou emissões de alertas. O serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent dá suporte à notificação de administradores através de operadores. Os operadores habilitam a notificação e o monitoramento de recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="operator-attributes-and-concepts"></a>Atributos e conceitos do operador  
Os atributos primários de um operador são:  
  
-   Nome do operador  
  
-   Informações de contato  
  
### <a name="naming-an-operator"></a>Nomeando um operador  
Todo operador deve ter um nome. Os nomes de operador devem ser exclusivos dentro da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e não podem ultrapassar **128** caracteres.  
  
### <a name="contact-information"></a>Informações de contato  
As informações de contato de um operador definem como ele é notificado. Os operadores podem ser notificados por email, pager ou através do comando **net send** :  
  
> [!IMPORTANT]
> As opções Pager e **net send** serão removidas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent em uma versão futura do [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar esses recursos em novo trabalho de desenvolvimento e planeje modificar os aplicativos que os usam atualmente.  
  
-   **Notificação por email**  
  
    A notificação por email envia uma mensagem de email ao operador. Para notificação por email, é necessário fornecer o endereço de email do operador.  
  
-   **Notificação por pager**  
  
    O envio de notificação por pager é implementado por email. Para notificação por pager, é necessário fornecer o endereço de email em que o operador recebe mensagens de pager. Para configurar notificação por pager, você deve instalar o software no servidor de email que processa a entrada de mensagens e convertê-las em mensagens de pager. O software pode aplicar várias abordagens, dentre as quais:  
  
    -   Encaminhar o email para um servidor de email remoto no site do provedor de pager.  
  
        O provedor de pager deve oferecer esse serviço, embora o software necessário geralmente esteja disponível como parte do sistema de email local. Para obter mais informações, consulte a documentação de seu pager.  
  
    -   Rotear o e-mail pela Internet para um servidor de e-mail no site do provedor de pager.  
  
        Esta é uma variação da primeira abordagem.  
  
    -   Processar o email de entrada e discar para o pager, por meio de um modem anexado.  
  
        Esse software é de propriedade dos provedores de serviços de pager. O software atua como um cliente de email que, periodicamente, processa sua caixa de entrada, interpretando todas ou parte das informações de endereço de email como número de pager ou correspondendo o nome do email a um número de pager em uma tabela de conversão.  
  
        Se todos os operadores compartilharem um provedor de pager, você poderá usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para especificar qualquer formatação de email especial necessária ao sistema de pager-para-email. A formatação especial pode ser um prefixo ou um sufixo e estar contida nas seguintes linhas do email:  
  
        **Assunto:**  
  
        **Cc**:  
  
        **Para**:  
  
    > [!NOTE]  
    > Se usar um sistema de pager alfanumérico, você poderá abreviar o texto enviado, excluindo o texto de erro da notificação por pager. Um exemplo de sistema de pager alfanumérico de baixa-capacidade é aquele limitado a 64 caracteres por página.  
  
-   **notificação net send**  
  
    Envia uma mensagem ao operador por meio do comando **net send** . Para **net send**, especifique o destinatário (computador ou usuário) de uma mensagem da rede.  
  
    > [!NOTE]  
    > O comando **net send** usa o Microsoft Windows Messenger. Para enviar alertas com êxito, esse serviço deve estar em execução em ambos os computadores, no computador em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executado e no computador utilizado pelo operador.  
  
## <a name="alerting-and-fail-safe-operators"></a>Alertas e operadores à prova de falhas  
Você pode escolher quais operadores serão notificados em resposta a um alerta. Por exemplo, você pode atribuir responsabilidades rotativas para a notificação de operadores agendando alertas. Por exemplo, o Indivíduo A é notificado sobre alertas que ocorrem às segundas, quartas ou sextas e o Indivíduo B, sobre alertas ocorridos às terças, quintas ou sábados.  
  
O operador à prova de falhas recebe uma notificação de alerta quando todas as notificações por pager aos operadores designados falham. Por exemplo, se você tiver definido três operadores para notificações por pager e nenhum deles puder ser alcançado via pager, o operador à prova de falhas será notificado.  
  
O operador à prova de falhas é notificado quando:  
  
-   Os operadores responsáveis pelo alerta não puderem ser informados por pager.  
  
    São motivos de falha em alcançar operadores primários endereços de pager incorretos e operadores fora de serviço.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Agent não consegue acessar as tabelas do sistema no banco de dados **msdb** .  
  
    A tabela do sistema **sysnotifications** especifica as responsabilidades de operador para os alertas.  
  
O operador à prova de falhas é um recurso de segurança. Não é possível excluir o operador atribuído à responsabilidade de proteção contra falhas sem reatribuí-la a outro operador ou excluir a atribuição junto com operador.  
  
## <a name="notifying-an-operator"></a>Notificando um operador  
É necessário configurar um ou mais destes itens para notificar um operador:  
  
-   Para enviar email com a funcionalidade Database Mail, é necessário ter acesso a um servidor de email que ofereça suporte a SMTP.  
  
-   Para paginação, é necessário ter software e/ou hardware de pager-para-email de terceiros.  
  
-   Para usar **net send**, o operador deve ter feito logon no computador especificado e este deve permitir mensagens do Windows Messenger.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**Tarefas**|**Tópico**|  
|Tarefas relacionadas à criação de um operador|[Criar um operador](../../ssms/agent/create-an-operator.md)<br /><br />[Designate a Fail-Safe Operator](../../ssms/agent/designate-a-fail-safe-operator.md)|  
|Tarefas relacionadas à atribuição de alertas|[Atribuir alertas a um operador](../../ssms/agent/assign-alerts-to-an-operator.md)<br /><br />[Definir a resposta a um alerta &#40;SQL Server Management Studio&#41;](../../ssms/agent/define-the-response-to-an-alert-sql-server-management-studio.md)<br /><br />[sp_add_notification (Transact-SQL)](https://msdn.microsoft.com/0525e0a2-ed0b-4e69-8a4c-a9e3e3622fbd)<br /><br />[Atribuir alertas a um operador](../../ssms/agent/assign-alerts-to-an-operator.md)|  
  
## <a name="see-also"></a>Consulte Também  
[Database Mail](../../relational-databases/database-mail/database-mail.md)  
  
