---
title: Conectar um banco de dados SQL do Azure (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.connsqlazure.f1
ms.assetid: 4e0344e9-1822-4698-ad22-05f1f341ced7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 94a830bba0339262148a0a7f826f3bcb89371274
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53372888"
---
# <a name="connect-to-an-azure-sql-database-ssas"></a>Conectar a um Banco de Dados SQL do Azure (SSAS)
  Esta página do **Assistente de Importação de Tabela** permite que você se conecte a um [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)]. Para acessar o assistente do [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], no menu **Modelo** , clique em **Importar de Fonte de Dados**.  
  
> [!NOTE]  
>  Se você estiver se conectando a um conjunto de dados do Azure DataMarket, consulte [Conectar-se a um relatório ou feed de dados &#40;SSAS&#41](connect-to-a-report-or-data-feed-ssas.md).  
  
 O [!INCLUDE[ssSDS](../includes/sssds-md.md)] é um banco de dados hospedado, relacional, a que você se conecta usando a Autenticação do SQL Server. Para obter mais informações sobre o [!INCLUDE[ssSDS](../includes/sssds-md.md)], consulte o site [Banco de dados SQL](https://go.microsoft.com/fwlink/?LinkID=157856). Para conectar uma fonte de dados, você deve ter o provedor apropriado instalado no computador.  
  
> [!NOTE]  
>  As credenciais do usuário atual são usadas na seleção de um banco de dados nesta página. Porém, a importação não terá êxito se o usuário especificado na página Informações sobre Representação não tiver privilégios suficientes para ler do banco de dados selecionado.  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 **Nome de conexão amigável**  
 Digite um nome exclusivo para esta conexão de fonte de dados. Esse é um campo obrigatório.  
  
 **Nome do servidor**  
 Digite o nome ou o endereço IP do servidor com o qual se conectar.  
  
 **Nome de usuário**  
 Especifique um nome de usuário para a conexão de banco de dados.  
  
 Este nome de usuário é usado ao construir a cadeia de conexão para a fonte de dados. Essas credenciais também são usadas na visualização e filtragem de dados na janela Propriedades de Tabela e no Assistente de Importação. Essas credenciais não são usadas para importar ou atualizar dados; em vez disso, utiliza-se as credenciais do Windows especificadas na página Informações sobre Representação.  
  
 **Senha**  
 Especifique uma senha para a conexão de banco de dados.  
  
 **Salvar minha senha**  
 Especifique se a senha que você inseriu na caixa **Senha** deve ser armazenada.  
  
 **Nome do banco de dados**  
 Selecione um banco de dados da lista de bancos de dados.  
  
 **Avançado**  
 Defina as propriedades de conexão adicionais usando a caixa de diálogo **Definir Propriedades Avançadas** . Para obter mais informações, consulte [Definir propriedades avançadas &#40;SSAS&#41;](set-advanced-properties-ssas.md).  
  
 **Testar Conexão**  
 Tente estabelecer uma conexão com a fonte de dados usando as configurações atuais. Uma mensagem que indica se a conexão foi bem-sucedida é exibida.  
  
  
