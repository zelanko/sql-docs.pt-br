---
title: Conectar-se ao MySQL (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 94099d01-ab19-4d58-a172-340c86b4a0f3
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 7289b3d5b287c1619a08921eba5cc30ff741e3b1
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52399899"
---
# <a name="connect-to-mysql-mysqltosql"></a>Conectar-se ao MySQL (MySQLToSQL)
Use o **conectar-se ao MySQL** caixa de diálogo para se conectar ao banco de dados MySQL que você deseja migrar.  
  
Para acessar essa caixa de diálogo, nos **arquivo** menu, selecione **conectar-se ao MySQL**. Se você tiver se conectado anteriormente, o comando é **reconectar-se ao MySQL**.  
  
## <a name="options"></a>Opções  
**Provedor**  
  
Provedor de MySQL disponível é Driver 5.1 ODBC do MySQL (confiável).  
  
**Modo**  
  
O modo padrão é o modo padrão. No modo padrão que você insira ou selecione valores para o MySQL, o nome do servidor, a porta do servidor, o nome de usuário e a senha.  
  
**Nome do servidor**  
  
Insira o nome do servidor MySQL. Essa é uma opção de modo padrão.  
  
**Porta do servidor**  
  
Insira a porta do servidor. A porta do servidor padrão é 3306. Essa é uma opção de modo padrão.  
  
**Nome de usuário**  
  
Insira o nome de usuário que usará o SSMA para se conectar ao banco de dados MySQL.  
  
**Senha**  
  
Digite a senha para o nome de usuário.  
  
**SSL**  
  
Se você quiser se conectar com segurança ao MySQL, certifique-se de usar de Secure Socket Layer (SSL), verificando a **SSL** caixa de seleção.  
  
**Configurar**  
  
Ele fornece uma opção para configurar a conexão ao MySQL por meio do Secure Socket Layer (SSL).  
  
> [!NOTE]  
> Para habilitar **configurar**, SSL deve ser definida como **verdadeiro**.  
  
Clicando no botão "Configurar", uma caixa de diálogo é exibida. Para usar a criptografia enquanto se conectar ao banco de dados MySQL, o caminho para os seguintes arquivos de três certificado presentes na caixa de diálogo deve ser definido [privacidade aprimorada Mail certificados (PEM)]:  
  
-   **Autoridade de certificação SSL:** Especifica o caminho para um arquivo com uma lista de confiança autoridades de certificação SSL.  
  
-   **Certificado SSL:** Especifica o nome do arquivo de certificado SSL a ser usado para estabelecer uma conexão segura.  
  
-   **CHAVE SSL:** Especifica o nome do arquivo de chave SSL a ser usado para estabelecer uma conexão segura.  
  
> [!NOTE]  
> -   O **Okey** botão é habilitado quando as informações necessárias foram fornecidas. Se qualquer um dos caminhos de arquivo for inválido, o botão "Okey" permanecerá desabilitado.  
> -   O **cancele** botão fecha a caixa de diálogo e **desativa** a opção SSL do formulário de Conexão principal.  
  
