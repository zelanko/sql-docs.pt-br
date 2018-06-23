---
title: Salve e Execute o pacote (Assistente de exportação e importação do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.impexpwizard.saveschedule.f1
ms.assetid: b582c462-3d7a-4a4c-a2a2-2c79fedab75a
caps.latest.revision: 39
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 6071acee5eb7d888bdf4182a30f433e531754f64
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36013588"
---
# <a name="save-and-execute-package-sql-server-import-and-export-wizard"></a>Salvar e Executar Pacote (Assistente de Importação e Exportação do SQL Server)
  Use o **salvar e executar pacote** caixa de diálogo para executar o pacote imediatamente, salve-o para ser executado posteriormente, ou ambos.  
  
> [!NOTE]  
>  Se você interromper um pacote antes de ele termina em execução, o pacote não será salvo, mesmo se você tiver selecionado o **salvar** caixa de seleção.  
  
 Para saber mais sobre este assistente, consulte [SQL Server Import and Export Wizard](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Para saber mais sobre as opções para iniciar o assistente, bem como as permissões necessárias para executar o assistente com êxito, consulte [executar o Assistente de exportação e importação do SQL Server](start-the-sql-server-import-and-export-wizard.md).  
  
 O objetivo do Assistente de Importação e Exportação do SQL Server é copiar dados de uma origem para um destino. O assistente também pode criar um banco de dados de destino e tabelas de destino para você. No entanto, se for necessário copiar vários bancos de dados ou tabelas, ou outros tipos de objetos de banco de dados, será necessário usar o Assistente para Copiar Banco de Dados. Para obter mais informações, consulte [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="options"></a>Opções  
 **Executar imediatamente**  
 Selecione esta opção para executar o pacote imediatamente.  
  
 **Salvar Pacote SSIS**  
 Salve o pacote para executá-lo posteriormente, com a opção de executá-lo imediatamente.  
  
> [!NOTE]  
>  Em [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], a opção para salvar o pacote criado pelo assistente não está disponível.  
  
 **SQL Server**  
 Selecione esta opção para salvar o pacote para o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `msdb` banco de dados.  
  
> [!NOTE]  
>  Essa opção só estará disponível se você tiver selecionado o **salvar pacote SSIS** opção.  
  
 **Sistema de arquivos**  
 Selecione esta opção para salvar o pacote como um arquivo com extensão .dtsx.  
  
> [!NOTE]  
>  Essa opção só estará disponível se você tiver selecionado o **salvar pacote SSIS** opção.  
  
 **Nível de Proteção do Pacote**  
 Selecione um nível de proteção na lista.  
  
 O nível de proteção determina o método de proteção, a senha ou a chave de usuário, bem como o escopo de proteção do pacote. A proteção pode incluir todos os dados ou apenas os dados confidenciais. Para entender os requisitos e opções de segurança de pacotes, consulte [controle de acesso de dados confidenciais em pacotes](../security/access-control-for-sensitive-data-in-packages.md) e [visão geral de segurança &#40;Integration Services&#41;](../security/security-overview-integration-services.md).  
  
> [!NOTE]  
>  Essa opção só estará disponível se você tiver selecionado o **salvar pacote SSIS** opção.  
  
 **Senha**  
 Digite uma senha.  
  
> [!NOTE]  
>  Essa opção só estará disponível se você tiver definido o **nível de proteção do pacote** opção **criptografar dados confidenciais com senha** ou **criptografar todos os dados com senha**.  
  
 **Digite a senha novamente**  
 Digite a senha novamente.  
  
> [!NOTE]  
>  Essa opção só estará disponível se você tiver definido o **nível de proteção do pacote** opção **criptografar dados confidenciais com senha** ou **criptografar todos os dados com senha**.  
  
## <a name="see-also"></a>Consulte também  
 [Execução de projetos e pacotes](../packages/run-integration-services-ssis-packages.md)   
 [Salvar pacotes](../save-packages.md)  
  
  