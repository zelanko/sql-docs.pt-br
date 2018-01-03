---
title: Conectar ao MySQL (MySQLToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-mysql
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 94099d01-ab19-4d58-a172-340c86b4a0f3
caps.latest.revision: "9"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 068fe6585eac87830511515a95373a938cbcdca2
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="connect-to-mysql-mysqltosql"></a>Conectar ao MySQL (MySQLToSQL)
Use o **conectar ao MySQL** caixa de diálogo para se conectar ao banco de dados MySQL que você deseja migrar.  
  
Para acessar essa caixa de diálogo, no **arquivo** menu, selecione **conectar ao MySQL**. Se você se conectou anteriormente, o comando é **reconectar ao MySQL**.  
  
## <a name="options"></a>Opções  
**Provedor**  
  
Provedor de MySQL disponível é MySQL ODBC 5.1 Driver (confiável).  
  
**Modo**  
  
O modo padrão é o modo padrão. No modo padrão você inserir ou selecionar valores para o MySQL, o nome do servidor, a porta do servidor, o nome de usuário e a senha.  
  
**Nome do servidor**  
  
Insira o nome do servidor MySQL. Essa é uma opção de modo padrão.  
  
**Porta do servidor**  
  
Insira a porta do servidor. A porta do servidor padrão é 3306. Essa é uma opção de modo padrão.  
  
**User name**  
  
Digite o nome de usuário SSMA usará para se conectar ao banco de dados MySQL.  
  
**Senha**  
  
Digite a senha para o nome de usuário.  
  
**SSL**  
  
Se você quiser se conectar com segurança ao MySQL, certifique-se de usar de Secure Socket Layer (SSL), verificando o **SSL** caixa de seleção.  
  
**Configurar**  
  
Ele fornece uma opção para configurar a conexão para MySQL por meio de Secure Socket Layer (SSL).  
  
> [!NOTE]  
> Para habilitar **configurar**, SSL deve ser definido como **True**.  
  
Em clicando no botão "Configurar", uma caixa de diálogo é exibida. Para usar a criptografia ao se conectar ao banco de dados MySQL, o caminho para os seguintes arquivos de três certificado presentes na caixa de diálogo deve ser definido [privacidade aprimorada Mail certificados (PEM)]:  
  
-   **Autoridade de certificação SSL:** Especifica o caminho para um arquivo com uma lista de relação de confiança de autoridades de certificação SSL.  
  
-   **Certificado SSL:** Especifica o nome do arquivo do certificado SSL a ser usado para estabelecer uma conexão segura.  
  
-   **CHAVE de SSL:** Especifica o nome do arquivo da chave SSL a ser usado para estabelecer uma conexão segura.  
  
> [!NOTE]  
> -   O **Okey** botão é habilitado quando as informações necessárias foi fornecidas. Se qualquer um dos caminhos de arquivo for inválido, o botão "Okey" permanecerá desabilitado.  
> -   O **Cancelar** botão fecha a caixa de diálogo e **desativa** a opção SSL do formulário de Conexão principal.  
  
