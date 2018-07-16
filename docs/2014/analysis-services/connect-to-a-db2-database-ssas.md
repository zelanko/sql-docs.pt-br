---
title: Conectar um banco de dados do DB2 (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.conndb2db.f1
ms.assetid: eeef3697-a4fd-4263-ba7e-f86afa1f46cc
caps.latest.revision: 10
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3952978ea68e1df54772f6a6065afd9fcb8d10b2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37200566"
---
# <a name="connect-to-a-db2-database-ssas"></a>Conectar a um banco de dados DB2 (SSAS)
  Esta página do **Assistente de Importação de Tabela** permite que você especifique as configurações de conexão a um banco de dados DB2. Para acessar o assistente do [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], no menu **Modelo** , clique em **Importar de Fonte de Dados**.  
  
 Para conectar uma fonte de dados, você deve ter o provedor apropriado instalado no computador.  
  
> [!NOTE]  
>  Quando você seleciona um banco de dados nesta página, são usadas as credenciais de usuário especificadas. Porém, a importação não terá êxito se o usuário especificado na página Informações sobre Representação não tiver privilégios suficientes para ler do banco de dados selecionado.  
  
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
  
 **Nome do banco de dados**  
 Selecione um banco de dados da lista de bancos de dados.  
  
 **Coleção de pacotes**  
 Especifique o nome da coleção de pacotes DB2. Um provedor usa pacotes para emitir instruções SQL e chamar procedimentos armazenados.  
  
 **Esquema Padrão**  
 Especifique o nome do esquema padrão para o banco de dados selecionado.  
  
 **Avançado**  
 Defina as propriedades de conexão adicionais usando a caixa de diálogo **Definir Propriedades Avançadas** .  
  
 **Testar Conexão**  
 Tente estabelecer uma conexão com a fonte de dados usando as configurações atuais. Uma mensagem que indica se a conexão foi bem-sucedida é exibida.  
  
  
