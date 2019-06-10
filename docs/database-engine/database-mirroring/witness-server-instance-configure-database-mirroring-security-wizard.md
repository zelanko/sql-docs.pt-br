---
title: Instância de servidor testemunha (Assistente para Configurar Segurança de Espelhamento de Banco de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.configdbmsecurwiz.witnsrvr.f1
ms.assetid: b5763663-984a-473b-93a3-6cd3322ad41c
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: e8d038947ac511d9b271fc5b4e07ffabcc47cc96
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66795072"
---
# <a name="witness-server-instance-configure-database-mirroring-security-wizard"></a>Instância de servidor testemunha (Assistente para Configurar Segurança de Espelhamento de Banco de Dados)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Use esta página para especificar as informações sobre a instância de servidor que servirá como a testemunha para a sessão.  
  
> [!NOTE]
>  Uma instância de servidor testemunha não está disponível em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Recursos com suporte nas edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 **Para configurar o espelhamento de banco de dados usando o SQL Server Management Studio**  
  
-   [Estabelecer uma sessão de espelhamento de banco de dados usando a Autenticação do Windows &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
-   [Iniciar o Assistente para Configurar Segurança de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)  
  
## <a name="options"></a>Opções  
 **Instância do servidor testemunha**  
 Se uma instância de servidor testemunha já for especificada (na página **Espelhamento** da caixa de diálogo **Propriedades do Banco de Dados** ), essa instância será exibida (para obter mais informações, veja [Propriedades do banco de dados &#40;página Espelhamento&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)).  
  
 Caso contrário, essa caixa de listagem exibir o nome do servidor atual. Observe que a instância de servidor testemunha não pode ser igual às instâncias do servidor principal ou espelho.  
  
 **Connect**  
 Se uma instância de servidor testemunha não foi especificada, clique em **Conectar**. Isso exibe a caixa de diálogo **Conectar ao Servidor** na qual você pode especificar a instância de servidor e estabelecer uma conexão.  
  
 Se a instância foi especificada, mas o assistente não tem uma conexão com permissão suficiente para verificar a existência do ponto de extremidade, clique em **Conectar**. Isso exibe a caixa de diálogo **Conectar ao Servidor** com a instância de servidor pré-selecionada e inalterável. Especifique uma conta de domínio com permissão suficiente e conecte-se à instância de servidor.  
  
> [!NOTE]  
>  Ao conectar-se à instância de servidor, o Assistente para Configurar Segurança de Espelhamento de Banco de Dados usa as credenciais fornecidas na caixa de diálogo **Conectar ao Servidor** . Essas credenciais são diferentes de uma sessão de espelhamento, que usa as credenciais da conta de inicialização onde a instância de servidor está sendo executada como um serviço.  
  
 **Porta do Ouvinte**  
 O comportamento dessa opção depende de o ponto de extremidade do espelhamento existir nessa instância do servidor, como segue:  
  
-   Se a porta do ouvinte não existir para a instância de servidor, o número da porta 5022 será exibido na caixa de texto **Porta** . Você pode digitar qualquer número de porta disponível, como 7022.  
  
-   Quando o ponto de extremidade do espelhamento já existir, o número da porta daquele ponto de extremidade será exibido. Se você precisar alterar aquela porta, use uma instrução ALTER ENDPOINT. Para obter mais informações, veja [ALTER ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md).  
  
    > [!NOTE]  
    >  É necessário um número de porta.  
  
 **Nome do ponto de extremidade**  
 Se o ponto de extremidade de espelhamento existir para essa instância do servidor, o nome de ponto de extremidade será exibido aqui. Se o ponto de extremidade não existir, você poderá especificar o nome do ponto de extremidade.  
  
 **Criptografar dados enviados por esse ponto de extremidade**  
 Por padrão, a criptografia está habilitada. Quando habilitada, a criptografia é necessária (não tem meramente um suporte) e usa os valores padrão de todas as opções de criptografia. Para obter mais informações, veja [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md).  
  
 Para desabilitar a criptografia, desmarque a caixa de seleção. Para habilitar a criptografia novamente, marque a caixa de seleção.  
  
## <a name="see-also"></a>Consulte Também  
 [O ponto de extremidade de espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [Propriedades do banco de dados &#40;página Espelhamento&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [Criar um ponto de extremidade de espelhamento de banco de dados para a Autenticação do Windows &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)   
 [Iniciar o Monitor de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [Espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [Testemunha de espelhamento de banco de dados](../../database-engine/database-mirroring/database-mirroring-witness.md)  
  
  
