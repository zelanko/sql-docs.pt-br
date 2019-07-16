---
title: Propriedades da coluna em modelos de tabela do Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 95a8f86b2cf2bc3cf28a128349540183c88d7fd0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68163106"
---
# <a name="column-properties"></a>Propriedades da coluna 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Este artigo descreve as propriedades de coluna do modelo de tabela.  
  
> [!NOTE]
>  Algumas propriedades não têm suporte em todos os níveis de compatibilidade.    
  
##  <a name="bkmk_properties"></a> Propriedades da coluna  
**Avançado**  
  
|Propriedade|Configuração padrão|Descrição|  
|--------------|---------------------|-----------------|  
|**Pasta de exibição**||Uma pasta única ou aninhada para organizar colunas em uma lista de campos do aplicativo cliente.|  

**Basic**  
  
|Propriedade|Configuração padrão|Descrição|  
|--------------|---------------------|-----------------|  
|**Nome da coluna**||O nome da coluna conforme é armazenada no modelo e como é exibida em uma lista de campo do cliente de relatório.|  
|**Formato de Dados**|Automaticamente determinado durante a importação.|Especifica o formato de exibição a ser usado para obter os dados nesta coluna. Essa propriedade oferece as seguintes opções:<br /><br /> **Geral**<br /><br /> **Número Decimal**<br /><br /> **Número Inteiro**<br /><br /> **Moeda**<br /><br /> **Porcentagem**<br /><br /> **Científico**<br /><br /> Depois que você definir um formato de dados, poderá definir as propriedades que são específicas a cada formato. Por exemplo, se você escolher o formato **Moedas** , poderá definir o número de casas decimais visíveis, escolher o separador de milhares e escolher o símbolo de moeda.<br /><br /> <br /><br /> Se os valores de coluna contiverem imagens, consulte **Imagem Representativa**.|  
|**Tipo de Dados**|Automaticamente determinado durante a importação.|Especifica o tipo de dados para todos os valores na coluna.|  
|**Descrição**||Uma descrição de texto para a coluna.<br /><br /> Em alguns clientes de relatório, se um usuário final colocar o cursor sobre esta coluna na lista de campos, a descrição aparecerá como uma dica de ferramenta.|  
|**Oculto**|False|Especifica se a coluna é ocultada das listas de campo de cliente de relatório.<br /><br /> Defina esta propriedade como **True** para ocultar esta coluna no vídeo. Por exemplo, as colunas que contêm identificadores ou chaves não são geralmente úteis para o usuário final.<br /><br /> Se você ocultar uma coluna do cliente de relatório, o campo não será suprimido nos dados de modelo. O campo ainda está visível se você criar uma consulta baseada no modelo. Uma coluna oculta ainda pode ser usada para agrupar ou classificar.<br /><br /> A propriedade **Oculta** não fornece nenhuma forma de proteção de dados. Para proteger os dados, use filtros de linha em Funções. Para obter mais informações, consulte [funções](../../analysis-services/tabular-models/roles-ssas-tabular.md).|  
|**Classificar por Coluna**||Especifica outra coluna para classificar os valores nesta coluna. Uma relação deve existir entre as duas colunas.<br /><br /> Este valor deve ser o nome de uma coluna existente. Você não pode especificar uma fórmula ou medida.|  
|**Exclusivo**||Pode ser definido para impor exclusividade dos valores na coluna. Sempre true para colunas calculadas, mesmo se a exclusividade é false.|  

 **Diversos**  
  
|Propriedade|Configuração padrão|Descrição|  
|--------------|---------------------|-----------------|  
|**Dicas de codificação**|Padrão|Especifica a codificação para otimizar o processamento. Codificação de valor pode melhorar o desempenho de consulta para colunas numéricas geralmente usadas em agregações. Codificação de hash é agrupar por colunas (geralmente valores de tabela de dimensões) e chaves estrangeiras. Colunas de cadeia de caracteres sempre são codificado de hash.|  

 **Propriedades de relatório**  
  
|Propriedade|Configuração padrão|Descrição|  
|--------------|---------------------|-----------------|  
|Imagem padrão|False|Especifica qual coluna fornece uma imagem que representa os dados de linha (por exemplo, uma ID de foto em um registro de funcionário).|  
|Rótulo Padrão|False|Especifica qual coluna fornece um nome para exibição para representar dados de linha (por exemplo, nome de funcionário em um registro de funcionário).|  
|URL de Imagem/Categoria de Dados (SP1)|False|Especifica o valor nesta coluna como um hiperlink para uma imagem em um servidor. Por exemplo: `http://localhost/images/image1.jpg`.|  
|Manter linhas exclusivas|False|Especifica quais colunas fornecem valores que devem ser tratados como exclusivos mesmo se forem duplicados (por exemplo, nome e sobrenome do funcionário, para casos onde dois ou mais funcionários têm o mesmo nome).|  
|Identificador de linha|False|Especifica uma coluna que só contém valores exclusivos, permitindo que seja usada como uma chave de agrupamento interna.|  
|Resumir por|Padrão|Especifica ferramentas de cliente de relatório aplicam a função de agregação SUM a cálculos de coluna quando essa coluna é adicionada a uma lista de campos. Para alterar o cálculo padrão, selecione-o na lista suspensa. Essa propriedade aplica-se somente a colunas do tipo que podem ser agregadas.|  
|Posição de detalhe da tabela|Não há conjunto de campos padrão|Especifica que essa coluna ou medida pode ser adicionada a um conjunto de campos de uma única tabela para aprimorar a experiência de visualização de tabela em um cliente de relatório.|  
  
##  <a name="bkmk_config_prop"></a> Definir as configurações de propriedade de coluna  
  
1.  No Designer de Modelo, em uma tabela, selecione uma coluna.  
  
2.  Na janela **Propriedades** , clique em uma propriedade e digite um valor ou clique na seta para baixo para selecionar uma opção de configuração.  
  
## <a name="see-also"></a>Confira também  
 [Propriedades de relatório do Power View](../../analysis-services/tabular-models/power-view-reporting-properties-ssas-tabular.md)   
 [Ocultar ou congelar colunas](../../analysis-services/tabular-models/hide-or-freeze-columns-ssas-tabular.md)   
 [Adicionar colunas a uma tabela](../../analysis-services/tabular-models/add-columns-to-a-table-ssas-tabular.md)  
  
  
