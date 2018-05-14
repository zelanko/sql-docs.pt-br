---
title: Propriedades de tabela | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c479fd46f5303d95e5c0390eb97246f8eeb08890
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="table-properties"></a>Table Properties 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Este artigo descreve as propriedades do modelo de tabela. As propriedades descritas aqui são diferentes daquelas na caixa de diálogo Editar Propriedades de Tabela, que definem quais colunas da origem são importadas.  
  
 Seções neste tópico:  
  
-   [Propriedades da tabela](#bkmk_properties)  
  
-   [Definir as configurações de propriedade da tabela](#bkmk_config_prop)  
  
##  <a name="bkmk_properties"></a> Propriedades da tabela  
 **Basic**  
  
|Propriedade|Configuração padrão|Description|  
|--------------|---------------------|-----------------|  
|**Nome da conexão**|\<nome da conexão >|O nome da conexão com a fonte de dados da tabela.<br /><br /> Para editar a conexão, clique no botão.|  
|**Oculto**|Falso|Especifica se a tabela é ocultada das listas de campo de cliente de relatório.|  
|**Partições**||As partições para a tabela não podem ser exibidas na janela **Propriedades** . Para exibir, criar ou editar partições, clique no botão para abrir o Gerenciador de Partições.|  
|**Dados de origem**||Os dados de origem da tabela não podem ser exibidos na janela **Propriedades** . Para exibir ou editar os dados de origem, clique no botão para abrir a caixa de diálogo Editar Propriedades da Tabela.|  
|**Descrição da tabela**||Uma descrição de texto da tabela.<br /><br /> No [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)], se um usuário final colocar o cursor sobre esta tabela na lista de campos, a descrição aparecerá como uma dica de ferramenta.|  
|**Nome da tabela**|\<nome amigável >|Especifica o nome amigável da tabela. O nome da tabela pode ser especificado quando uma tabela é importada com o uso do Assistente de Importação de Tabela ou a qualquer momento após a importação. O nome da tabela no modelo pode ser diferente da tabela associada na origem. O nome amigável da tabela aparece na lista de campos do aplicativo cliente de relatório e no banco de dados modelo no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].|  
  
 **Propriedades de relatório**  
  
 Para obter descrições detalhadas e informações de configuração de propriedades de relatório, consulte [propriedades de relatório do Power View](../../analysis-services/tabular-models/power-view-reporting-properties-ssas-tabular.md).  
  
|Propriedade|Configuração padrão|Description|  
|--------------|---------------------|-----------------|  
|**Conjunto de Campos Padrão**|||  
|Comportamento de tabela|||  
  
##  <a name="bkmk_config_prop"></a> Definir as configurações de propriedade da tabela  
  
1.  No designer de modelos, na Exibição de Dados, clique em uma tabela (guia) ou, na Exibição de Diagrama, clique em um cabeçalho de tabela.  
  
2.  Na janela **Propriedades** , clique em uma propriedade e digite um valor ou clique no botão para obter opções de configuração adicionais.  
  
  
