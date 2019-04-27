---
title: Instância do servidor espelho (Assistente para Configurar Segurança de Espelhamento de Banco de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.configdbmsecurwiz.mirrorsrvr.f1
ms.assetid: 53223432-615e-440f-904d-925d33ec2144
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 83a92633a4c466e72c8cc2de0cc1c220e88e01bb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62755162"
---
# <a name="mirror-server-instance-configure-database-mirroring-security-wizard"></a>Instância de servidor espelho (Assistente para Configurar Segurança de Espelhamento de Banco de Dados)
  Use esta página para especificar informações sobre a instância de servidor com o banco de dados espelho.  
  
> [!IMPORTANT]  
>  A instância do servidor espelho deve estar executando a mesma edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Standard ou Enterprise, como a instância do servidor principal. Além disso, é altamente recomendável que elas sejam executadas em sistemas comparáveis que possam controlar cargas de trabalho idênticas.  
  
 **Para configurar o espelhamento de banco de dados usando o SQL Server Management Studio**  
  
-   [Estabelecer uma sessão de espelhamento de banco de dados usando a Autenticação do Windows &#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md)  
  
-   [Iniciar o Assistente para Configurar Segurança de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](start-the-configuring-database-mirroring-security-wizard.md)  
  
## <a name="options"></a>Opções  
 **Instância do servidor espelho**  
 Se uma instância de servidor espelho já for especificada (na página **Espelhamento** da caixa de diálogo **Propriedades do Banco de Dados** ), essa instância será exibida; para obter mais informações, veja [Propriedades do banco de dados &#40;página Espelhamento&#41;](../../relational-databases/databases/database-properties-mirroring-page.md).  
  
 Caso contrário, insira o nome da instância de servidor espelho. Observe que a instância de servidor espelho não pode ser igual à instância de servidor principal.  
  
 **Connect**  
 Se uma instância de servidor espelho não foi especificada, clique em **Conectar**. Isso exibe a caixa de diálogo **Conectar ao Servidor** na qual você pode especificar a instância de servidor e estabelecer uma conexão.  
  
 Se a instância foi especificada, mas o assistente não tem uma conexão com permissão suficiente para verificar a existência do ponto de extremidade, clique em **Conectar**. Isso exibe a caixa de diálogo **Conectar ao Servidor** com a instância de servidor pré-selecionada e inalterável. Especifique uma conta de domínio com permissão suficiente e conecte-se à instância de servidor.  
  
> [!NOTE]  
>  Ao conectar-se à instância de servidor, o Assistente para Configurar Segurança de Espelhamento de Banco de Dados usa as credenciais fornecidas na caixa de diálogo **Conectar ao Servidor** . Essas credenciais são diferentes de uma sessão de espelhamento, que usa as credenciais da conta de inicialização onde a instância de servidor está sendo executada como um serviço.  
  
 **Porta do Ouvinte**  
 O comportamento dessa opção depende de o ponto de extremidade do espelhamento existir nessa instância do servidor, como segue:  
  
-   Se uma porta do ouvinte não existir para a instância de servidor, o número da porta 5022 será exibido na caixa de texto **Porta** . Você pode usar qualquer número de porta disponível, como 7022.  
  
-   Quando o ponto de extremidade do espelhamento já existir, o número da porta daquele ponto de extremidade é exibido. Se for necessário alterar a porta, use um comando ALTER ENDPOINT. Para obter mais informações, veja [ALTER ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-endpoint-transact-sql).  
  
    > [!NOTE]  
    >  É necessário um número de porta.  
  
 **Nome do ponto de extremidade**  
 Se o ponto de extremidade de espelhamento existir para essa instância do servidor, o nome de ponto de extremidade será exibido aqui. Se o ponto de extremidade não existir, você poderá especificar o nome do ponto de extremidade.  
  
 **Criptografar dados enviados por esse ponto de extremidade**  
 Por padrão, a criptografia está habilitada. Quando habilitada, a criptografia é necessária (não tem meramente um suporte) e usa os valores padrão de todas as opções de criptografia. Para obter mais informações, veja [CREATE ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql).  
  
 Para desabilitar a criptografia, desmarque a caixa de seleção. Para habilitar a criptografia novamente, marque a caixa de seleção.  
  
## <a name="see-also"></a>Consulte também  
 [O ponto de extremidade de espelhamento de banco de dados &#40;SQL Server&#41;](the-database-mirroring-endpoint-sql-server.md)   
 [Propriedades do banco de dados &#40;página Espelhamento&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [Criar um ponto de extremidade de espelhamento de banco de dados para a Autenticação do Windows &#40;Transact-SQL&#41;](create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)   
 [Iniciar o Monitor de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](../database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [Espelhamento de banco de dados &#40;SQL Server&#41;](database-mirroring-sql-server.md)  
  
  
