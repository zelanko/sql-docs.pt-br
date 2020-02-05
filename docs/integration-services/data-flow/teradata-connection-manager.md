---
title: Usar o gerenciador de conexões do Teradata | Microsoft Docs
ms.custom: ''
ms.date: 11/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d520f83f515694bd8852ce11ea13fce7f3213596
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75245120"
---
# <a name="use-the-teradata-connection-manager"></a>Use o gerenciador de conexões do Teradata

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

Com o gerenciador de conexões do Teradata, você pode habilitar um pacote para extrair dados de bancos de dado do Teradata e carregar dados para o bancos de dado Teradata.

Você define a propriedade `ConnectionManagerType` do gerenciador de conexões do Teradata como *TERADATA*.

## <a name="configure-the-teradata-connection-manager"></a>Configurar o gerenciador de conexões do Teradata

As alterações de configuração do gerenciador de conexões são resolvidas pelos Integration Services no runtime. Para adicionar uma conexão a uma fonte de dados Teradata, preencha as informações no painel **Editor do Gerenciador de Conexões do Teradata**.

![O painel do Editor do Gerenciador de Conexões do Teradata](media/teradata-connection-manager.png)

1. Na caixa **Nome**, digite um nome para essa conexão. O nome padrão é **Gerenciador de Conexões do Teradata**.

1. (Opcional) Na caixa **Descrição**, insira uma descrição da conexão.

1. Na caixa **Nome do servidor**, digite o nome do servidor Teradata ao qual se conectar.

1. Em **Autenticação**, siga um destes procedimentos:

   - Para usar a autenticação do Windows, selecione **Usar Autenticação do Windows**.
   - Para usar a autenticação de banco de dados do Teradata, selecione **Usar a autenticação do Teradata** e, em seguida, insira as seguintes credenciais para esse tipo de autenticação:
     - Na caixa **Mecanismo**, insira o mecanismo de verificação de segurança que você deseja usar. Os valores de mecanismo válidos incluem TD1, TD2, LDAP, KRB5, KRB5C, NTLM e NTLMC.
     - Na caixa **Parâmetro**, insira os tipos de parâmetros necessários para o mecanismo de verificação de segurança que você inseriu.
     - Na caixa **Nome de usuário**, digite o nome que você usa para se conectar ao banco de dados do Teradata.  
     - Na caixa **Senha**, insira a senha do banco de dados do Teradata do usuário.

1. (Opcional) Na lista suspensa **Banco de dados padrão**, selecione o banco de dados do Teradata ao qual se conectar. Se essa permissão de acesso ao banco de dados estiver incorreta, um erro será exibido e você poderá inserir manualmente o nome do banco de dados.

1. (Opcional) Na caixa **Conta**, digite o nome da conta que corresponde ao nome de usuário. Se esse valor estiver vazio, será usada a conta para o proprietário imediato do banco de dados.
1. Selecione **OK**.

## <a name="custom-property"></a>Propriedade personalizada

A propriedade personalizada `UseUTF8CharSet` especifica se o conjunto de caracteres UTF-8 é usado. O valor padrão é *True*.

Para definir a propriedade:

1. Abra o SSDT (SQL Server Data Tools).
1. Na área **Gerenciador de Conexões**, clique com o botão direito do mouse em **Gerenciador de Conexões do Teradata** e selecione **Propriedades**.
1. No painel **Propriedades**, para a propriedade `UseUTF8CharSet`, selecione *True* ou *False*.

## <a name="troubleshoot-the-teradata-connection-manager"></a>Solucionar problemas do gerenciador de conexões do Teradata

Para registrar em log chamadas do gerenciador de conexões do Teradata para o driver ODBC (Open Database Connectivity) do Teradata, habilite o rastreamento ODBC do Windows no Administrador de Fonte de Dados ODBC do Windows.

## <a name="next-steps"></a>Próximas etapas

- Configurar a [Origem do Teradata](teradata-source.md).
- Configure o [Destino do Teradata](teradata-destination.md).
- Em caso de dúvidas, acesse a [Tech Community](https://aka.ms/AA5u35j).
