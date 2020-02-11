---
title: Conectar-se ao Microsoft SQL Server Analysis Services (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.connsqlserveras.f1
ms.assetid: 7f3244ee-b690-471c-893d-68e361c2d416
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fe8eee02d019b5cf68e257b3fac4266a18ead795
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66087025"
---
# <a name="connect-to-microsoft-sql-server-analysis-services-ssas"></a>Conectar ao Microsoft SQL Server Analysis Services (SSAS)
  Esta página do **Assistente de Importação de Tabela** o habilita a especificar configurações para importar dados de um cubo do Microsoft SQL Server Analysis Services ou de uma pasta de trabalho PowerPivot que esteja hospedada no SharePoint. Para acessar o assistente do [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], no menu **Modelo** , clique em **Importar de Fonte de Dados**.  
  
 Para conectar uma fonte de dados, você deve ter o provedor apropriado instalado no computador.  
  
> [!NOTE]  
>  As credenciais do usuário atual são usadas na seleção de um banco de dados nesta página. Porém, a importação não terá êxito se o usuário especificado na página Informações sobre Representação não tiver privilégios suficientes para ler do banco de dados selecionado.  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 **Nome de conexão amigável**  
 Digite um nome exclusivo para esta conexão de fonte de dados. Esse é um campo obrigatório.  
  
 **Nome do Servidor ou Arquivo**  
 Insira um dos seguintes:  
  
-   Digite o nome ou o endereço IP do servidor do SQL Server Analysis Services ao qual se conectar.  
  
     Você pode usar um ponto (.), (local) ou localhost para indicar o servidor local.  
  
-   Digite a URL de uma pasta de trabalho do PowerPivot publicada no SharePoint.  
  
 **Usar autenticação do Windows**  
 Especifique se a Autenticação do Windows será usada para conectar a um servidor do SQL Server Analysis Services.  
  
 O modo de Autenticação do Windows permite que um usuário se conecte por meio de uma conta de usuário do Windows. Sempre que for possível, use a Autenticação do Windows.  
  
 Quando a Autenticação do Windows é usada, as credenciais do usuário atual são usadas na visualização e filtragem de dados na janela Propriedades de Tabela e no Assistente de Importação. Essas credenciais não são usadas para importar ou atualizar dados; em vez disso, utiliza-se as credenciais do Windows especificadas na página Informações sobre Representação.  
  
 **Usar autenticação SQL Server**  
 Especifique se a Autenticação do SQL Server será usada para conectar a um servidor do SQL Server Analysis Services.  
  
 Com a Autenticação do SQL Server, o próprio SQL Server executa a autenticação verificando se foi configurada uma conta de logon do SQL Server e se a senha especificada corresponde a uma senha registrada anteriormente.  
  
 A Autenticação do SQL Server é usada para construir a cadeia de conexão para a fonte de dados. Essas credenciais também são usadas na visualização e filtragem de dados na janela Propriedades de Tabela e no Assistente de Importação. Essas credenciais não são usadas para importar ou atualizar dados; em vez disso, utiliza-se as credenciais do Windows especificadas na página Informações sobre Representação.  
  
 **Nome de usuário**  
 Especifique um nome de usuário para a conexão de banco de dados. Essa opção estará disponível somente se você decidiu conectar-se usando a Autenticação do Windows.  
  
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
  
  
