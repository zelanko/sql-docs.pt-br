---
title: Se conectar a um banco de dados do Microsoft SQL Server (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.connsqlserverdb.f1
ms.assetid: 6ebfe029-dbba-4f0d-a556-328e79ef629f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6e3015f589f40dfc8bafc30da3a30316004f086a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62680177"
---
# <a name="connect-to-a-microsoft-sql-server-database-ssas"></a>Conectar a um banco de dados Microsoft SQL Server (SSAS)
  Esta página do **Assistente de Importação de Tabela** o habilita a especificar as configurações de conexão a um banco de dados do Microsoft SQL Server. Para acessar o assistente do [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], no menu **Modelo** , clique em **Importar de Fonte de Dados**.  
  
 Para conectar uma fonte de dados, você deve ter o provedor apropriado instalado no computador.  
  
> [!NOTE]  
>  As credenciais do usuário atual são usadas na seleção de um banco de dados nesta página. Porém, a importação não terá êxito se o usuário especificado na página Informações sobre Representação não tiver privilégios suficientes para ler do banco de dados selecionado.  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 **Nome de conexão amigável**  
 Digite um nome exclusivo para esta conexão de fonte de dados. Esse é um campo obrigatório.  
  
 **Nome do servidor**  
 Selecione ou digite o nome ou o endereço IP da instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] à qual se conectar.  
  
 Você pode usar um ponto (.), (local) ou localhost para indicar o servidor local.  
  
 **Usar Autenticação do Windows**  
 Especifique se a Autenticação do Windows será usada para estabelecer conexão com uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 O modo de Autenticação do Windows habilita um usuário a se conectar por meio de uma conta de usuário do Windows. Sempre que for possível, use a Autenticação do Windows.  
  
 Quando a Autenticação do Windows é usada, as credenciais do usuário atual são usadas na visualização e filtragem de dados na janela Propriedades de Tabela e no Assistente de Importação. Essas credenciais não são usadas para importar ou atualizar dados; em vez disso, utiliza-se as credenciais do Windows especificadas na página Informações sobre Representação.  
  
 **Usar Autenticação do SQL Server**  
 Especifique se a Autenticação do SQL Server será usada para estabelecer conexão com uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 Com a Autenticação do SQL Server, o próprio SQL Server executa a autenticação verificando se foi configurada uma conta de logon do SQL Server e se a senha especificada corresponde a uma senha registrada anteriormente.  
  
 A Autenticação do SQL Server é usada para construir a cadeia de conexão para a fonte de dados. Essas credenciais também são usadas na visualização e filtragem de dados na janela Propriedades de Tabela e no Assistente de Importação. Essas credenciais não são usadas para importar ou atualizar dados; em vez disso, utiliza-se as credenciais do Windows especificadas na página Informações sobre Representação.  
  
 **Nome de usuário**  
 Especifique um nome de usuário para a conexão de banco de dados. Esta opção só estará disponível se você tiver optado por conectar-se usando a Autenticação do SQL Server.  
  
 **Senha**  
 Especifique uma senha para a conexão de banco de dados. Esta opção só poderá ser editada se você tiver optado por conectar-se usando a Autenticação do SQL Server.  
  
 **Salvar minha senha**  
 Especifique se a senha que você inseriu na caixa **Senha** deve ser armazenada. Esta opção só estará disponível se você tiver optado por conectar-se usando a Autenticação do SQL Server.  
  
 **Nome do banco de dados**  
 Selecione um banco de dados da lista de bancos de dados.  
  
 **Avançado**  
 Defina as propriedades de conexão adicionais usando a caixa de diálogo **Definir Propriedades Avançadas** . Para obter mais informações, consulte [Definir propriedades avançadas &#40;SSAS&#41;](set-advanced-properties-ssas.md).  
  
 **Testar Conexão**  
 Tente estabelecer uma conexão com a fonte de dados usando as configurações atuais. Uma mensagem que indica se a conexão foi bem-sucedida é exibida.  
  
  
