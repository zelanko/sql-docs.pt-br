---
title: Conectar um banco de dados do Sybase (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.connsybasedb.f1
ms.assetid: b4ebdc57-8b2a-4950-b489-88360e6c82c5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 01b011ba7b321252f90f74289cfe13a2257f2ea3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48074086"
---
# <a name="connect-to-a-sybase-database-ssas"></a>Conectar a um banco de dados Sybase (SSAS)
  Esta página do **Assistente de Importação de Tabela** o habilita a especificar as configurações de conexão a um banco de dados Sybase. Para acessar o assistente do [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], no menu **Modelo** , clique em **Importar de Fonte de Dados**.  
  
 Para conectar uma fonte de dados, você deve ter o provedor apropriado instalado no computador.  
  
> [!NOTE]  
>  As credenciais do usuário atual são usadas na seleção de um banco de dados nesta página. Porém, a importação não terá êxito se o usuário especificado na página Informações sobre Representação não tiver privilégios suficientes para ler do banco de dados selecionado.  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 **Nome de conexão amigável**  
 Digite um nome exclusivo para esta conexão de fonte de dados. Esse é um campo obrigatório.  
  
 **Nome do servidor**  
 Digite ou selecione a instância do servidor com a qual se conectar.  
  
 **Nome de usuário**  
 Especifique um nome de usuário para a conexão de banco de dados.  
  
 Este nome de usuário é usado ao construir a cadeia de conexão para a fonte de dados. Essas credenciais também são usadas na visualização e filtragem de dados na janela Propriedades de Tabela e no Assistente de Importação. Essas credenciais não são usadas para importar ou atualizar dados; em vez disso, utiliza-se as credenciais do Windows especificadas na página Informações sobre Representação.  
  
 **Senha**  
 Especifique uma senha para a conexão de banco de dados.  
  
 **Salvar minha senha**  
 Especifique se a senha que você inseriu na caixa **Senha** deve ser armazenada.  
  
 **Database Name**  
 Selecione um banco de dados da lista de bancos de dados.  
  
 **Avançado**  
 Defina as propriedades de conexão adicionais usando a caixa de diálogo **Definir Propriedades Avançadas** . Para obter mais informações, consulte [Definir propriedades avançadas &#40;SSAS&#41;](set-advanced-properties-ssas.md).  
  
 **Testar Conexão**  
 Tente estabelecer uma conexão com a fonte de dados usando as configurações atuais. Uma mensagem que indica se a conexão foi bem-sucedida é exibida.  
  
  
