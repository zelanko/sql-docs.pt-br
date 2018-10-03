---
title: Salvar e executar pacote (Assistente de exportação e importação do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.saveschedule.f1
ms.assetid: b582c462-3d7a-4a4c-a2a2-2c79fedab75a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: de6560f7bc91a76652be5ca198a91c4ab9c1f1af
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48104497"
---
# <a name="save-and-execute-package-sql-server-import-and-export-wizard"></a>Salvar e Executar Pacote (Assistente de Importação e Exportação do SQL Server)
  Use o **salvar e executar pacote** caixa de diálogo para executar o pacote imediatamente, salve-o para executar posteriormente ou ambos.  
  
> [!NOTE]  
>  Se você interromper um pacote antes de ele fim da execução, o pacote não será salvo, mesmo se você selecionou o **salvar** caixa de seleção.  
  
 Para saber mais sobre este assistente, consulte [SQL Server Import and Export Wizard](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Para saber mais sobre as opções para iniciar o assistente, bem como as permissões necessárias para executar o assistente com êxito, consulte [executar o Assistente de exportação e importação do SQL Server](start-the-sql-server-import-and-export-wizard.md).  
  
 O objetivo do Assistente de Importação e Exportação do SQL Server é copiar dados de uma origem para um destino. O assistente também pode criar um banco de dados de destino e tabelas de destino para você. No entanto, se for necessário copiar vários bancos de dados ou tabelas, ou outros tipos de objetos de banco de dados, será necessário usar o Assistente para Copiar Banco de Dados. Para obter mais informações, consulte [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="options"></a>Opções  
 **Executar imediatamente**  
 Selecione esta opção para executar o pacote imediatamente.  
  
 **Salvar Pacote SSIS**  
 Salve o pacote para executá-lo posteriormente, com a opção de executá-lo imediatamente.  
  
> [!NOTE]  
>  No [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], a opção para salvar o pacote criado pelo assistente não está disponível.  
  
 **SQL Server**  
 Selecione esta opção para salvar o pacote para o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `msdb` banco de dados.  
  
> [!NOTE]  
>  Essa opção está disponível apenas se você tiver selecionado a **salvar pacote SSIS** opção.  
  
 **Sistema de arquivos**  
 Selecione esta opção para salvar o pacote como um arquivo com extensão .dtsx.  
  
> [!NOTE]  
>  Essa opção está disponível apenas se você tiver selecionado a **salvar pacote SSIS** opção.  
  
 **Nível de Proteção do Pacote**  
 Selecione um nível de proteção na lista.  
  
 O nível de proteção determina o método de proteção, a senha ou a chave de usuário, bem como o escopo de proteção do pacote. A proteção pode incluir todos os dados ou apenas os dados confidenciais. Para entender os requisitos e opções de segurança de pacotes, consulte [controle de acesso para dados confidenciais em pacotes](../security/access-control-for-sensitive-data-in-packages.md) e [visão geral de segurança &#40;Integration Services&#41;](../security/security-overview-integration-services.md).  
  
> [!NOTE]  
>  Essa opção está disponível apenas se você tiver selecionado a **salvar pacote SSIS** opção.  
  
 **Senha**  
 Digite uma senha.  
  
> [!NOTE]  
>  Essa opção só estará disponível se você tiver definido o **nível de proteção do pacote** opção **criptografar dados confidenciais com senhas** ou **criptografar todos os dados com senhas**.  
  
 **Digite a senha novamente**  
 Digite a senha novamente.  
  
> [!NOTE]  
>  Essa opção só estará disponível se você tiver definido o **nível de proteção do pacote** opção **criptografar dados confidenciais com senhas** ou **criptografar todos os dados com senhas**.  
  
## <a name="see-also"></a>Consulte também  
 [Execução de projetos e pacotes](../packages/run-integration-services-ssis-packages.md)   
 [Salvar pacotes](../save-packages.md)  
  
  
