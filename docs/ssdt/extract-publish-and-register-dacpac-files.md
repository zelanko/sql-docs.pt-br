---
title: Extrair, publicar e registrar arquivos .dacpac | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.DacTableChooser
- sql.data.tools.DacPublishDialog
- sql.data.tools.DacPropertiesDialog
- sql.data.tools.publishdacproject
- sql.data.tools.DacExtractDialog
ms.assetid: ed900f93-d3df-40f5-8e62-4d722595e041
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2aee0f145c2ef2b82b929a8f6358a764a10050f5
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70154798"
---
# <a name="extract-publish-and-register-dacpac-files"></a>Extrair, publicar e registrar arquivos .dacpac
Este tópico descreve quatro procedimentos que você pode realizar clicando com o botão direito do mouse em um banco de dados conectado no Pesquisador de Objetos do SQL Server:  
  
-   Publicar aplicativo da camada de dados  
  
-   Extrair aplicativo da camada de dados  
  
-   Registrar aplicativo da camada de dados  
  
-   Cancelar o registro de aplicativo da camada de dados  
  
## <a name="publish-data-tier-application"></a>Publicar aplicativo da camada de dados  
Você pode publicar um banco de dados .dacpac. A ação de publicar atualiza um esquema de banco de dados incrementalmente para que corresponda ao esquema de um arquivo .dacpac de origem. Se o banco de dados não existir no servidor, a operação de publicação irá criá-lo.  
  
Essa ação também está disponível selecionando o nó Bancos de Dados.  
  
Selecionar o arquivo .dacpac. Depois de especificar um arquivo .dacpac, o botão **Propriedades do DAC** estará habilitado. A caixa de diálogo **Propriedades do DAC** exibe informações sobre o arquivo .dacpac.  
  
Especifique a cadeia de conexão para o servidor de banco de dados e, em seguida, especifique o nome do banco de dados, se o nome do banco de dados não estiver na cadeia de conexão.  
  
Os botões **Publicar** e **Gerar Script** agora estão habilitados. Se você gerar um script, ele será aberto em uma janela de documento e poderá ser salvo conforme o necessário. Se você escolher publicar diretamente no banco de dados, um resumo da atualização e o script real usado poderão ser exibidos na janela **Operações de Ferramentas de Dados**.  
  
Quando marcada, a caixa de seleção **Registrar como um Aplicativo da Camada de Dados** faz o banco de dados resultante ser registrado como um aplicativo da camada de dados nos metadados do servidor. Se o banco de dados no qual você está publicando estiver registrado, você poderá causar a falha na publicação se o esquema do banco de dados for diferente de seu dacpac registrado atual.  
  
A configuração de publicação adicional está disponível na caixa de diálogo **Configurações de Publicação Avançadas**, que você pode acessar clicando no botão **Avançado**.  
  
## <a name="extract-data-tier-application"></a>Extrair aplicativo da camada de dados  
Você pode extrair um .dacpac de um banco de dados. A extração cria um arquivo de instantâneo de banco de dados (.dacpac) de um banco de dados dinâmico do SQL Server ou um Banco de dados SQL do Azure que pode conter dados de tabelas de usuários, além do esquema de banco de dados.  
  
Especifique o arquivo .dacpac para ser criado. O botão **Propriedades do DAC** exibe a caixa de diálogo **Propriedades do AC**, que permite especificar as propriedades do arquivo .dacpac.  
  
Modifique, conforme o necessário, a configuração do processo de extração. Na seção **Configurações de Extração**, você pode escolher extrair o esquema somente ou extrair o esquema e incluir dados da tabela. Se você escolher extrair o esquema e os dados, poderá selecionar as tabelas para as quais você gostaria de extrair dados.  
  
## <a name="register-data-tier-application"></a>Registrar aplicativo da camada de dados  
Você pode registrar um banco de dados como um aplicativo de camada de dados (DAC) dentro da instância. Isso armazena a representação do estado atual do esquema de bancos de dados nos metadados do sistema.  
  
Na caixa de diálogo **Registrar aplicativo da camada de dados**, especifique as propriedades do DAC registrado.  
  
## <a name="unregister-data-tier-application"></a>Cancelar o registro de aplicativo da camada de dados  
Cancelar o registro permite remover da instância os metadados para um aplicativo de camada de dados registrada. Cancelar o registro não exclui o banco de dados registrado.  
  
## <a name="see-also"></a>Consulte Também  
[Desenvolvimento de banco de dados conectado](../ssdt/connected-database-development.md)  
  
