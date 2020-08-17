---
description: Conectar-se ao MySQL (MySQLToSQL)
title: Conectar-se ao MySQL (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 94099d01-ab19-4d58-a172-340c86b4a0f3
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 399946496bbb649f84c9d539a9fe80f3f7919b31
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88372692"
---
# <a name="connect-to-mysql-mysqltosql"></a>Conectar-se ao MySQL (MySQLToSQL)
Use a caixa de diálogo **conectar-se ao MySQL** para se conectar ao banco de dados MySQL que você deseja migrar.  
  
Para acessar essa caixa de diálogo, no menu **arquivo** , selecione **conectar-se ao MySQL**. Se você tiver se conectado anteriormente, o comando será **reconectado ao MySQL**.  
  
## <a name="options"></a>Opções  
**Provedor**  
  
O provedor MySQL disponível é um driver do MySQL ODBC 5,1 (confiável).  
  
**Modo**  
  
O modo padrão é o modo padrão. No modo padrão, você insere ou seleciona valores para o MySQL, o nome do servidor, a porta do servidor, o nome de usuário e a senha.  
  
**Nome do servidor**  
  
Insira o nome do servidor MySQL. Essa é uma opção de modo padrão.  
  
**Porta do servidor**  
  
Insira a porta do servidor. A porta padrão do servidor é 3306. Essa é uma opção de modo padrão.  
  
**Nome de usuário**  
  
Insira o nome de usuário que o SSMA usará para se conectar ao banco de dados MySQL.  
  
**Senha**  
  
Digite a senha para o nome de usuário.  
  
**SSL**  
  
Se você quiser se conectar com segurança ao MySQL, faça o uso da SSL (Secure Socket Layer) marcando a caixa de seleção **SSL** .  
  
**Configure**  
  
Ele fornece uma opção para configurar a conexão com o MySQL por meio do protocolo SSL.  
  
> [!NOTE]  
> Para habilitar **Configurar**, o SSL deve ser definido como **true**.  
  
Ao clicar no botão "configurar", uma caixa de diálogo é exibida. Para usar a criptografia ao se conectar ao banco de dados MySQL, o caminho para os três arquivos de certificado a seguir presentes na caixa de diálogo deve ser definido [certificados de Privacy Enhanced Mail (PEM)]:  
  
-   **Autoridade de certificação SSL:** Especifica o caminho para um arquivo com uma lista de autoridades de certificação SSL de confiança.  
  
-   **Certificado SSL:** Especifica o nome do arquivo de certificado SSL a ser usado para estabelecer uma conexão segura.  
  
-   **chave SSL:** Especifica o nome do arquivo de chave SSL a ser usado para estabelecer uma conexão segura.  
  
> [!NOTE]  
> -   O botão **OK** é habilitado quando as informações necessárias foram fornecidas. Se qualquer um dos caminhos de arquivo for inválido, o botão "OK" permanecerá desabilitado.  
> -   O botão **Cancelar** fecha a caixa de diálogo e **DESATIVA** a opção SSL do formulário de conexão principal.  
  
