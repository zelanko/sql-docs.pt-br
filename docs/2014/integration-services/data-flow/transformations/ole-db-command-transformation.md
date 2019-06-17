---
title: Transformação Comando OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.oledbcommandtrans.f1
helpviewer_keywords:
- statements [Integration Services]
- OLE DB Command transformation
ms.assetid: baa6735c-5acf-4759-b077-1216aca16c6c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3a8ffc33de161c71c6f72eebf8616d1e814fb994
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62770382"
---
# <a name="ole-db-command-transformation"></a>transformação Comando OLE DB
  A transformação Comando OLE DB executa uma instrução SQL para cada linha do fluxo de dados. Por exemplo, você pode executar uma instrução SQL que insira, atualize ou exclua linhas em uma tabela de banco de dados.  
  
 É possível configurar a transformação Comando OLE DB com os seguintes procedimentos:  
  
-   Forneça a instrução SQL que a transformação executa para cada linha.  
  
-   Especifique o número de segundos antes que a instrução SQL expire.  
  
-   Especifique a página de código padrão.  
  
 Normalmente, a instrução SQL inclui parâmetros. Os valores de parâmetro são armazenados em colunas externas na entrada da transformação e o mapeamento de uma coluna de entrada para uma coluna externa mapeia uma coluna de entrada para um parâmetro. Por exemplo, para localizar linhas na tabela **DimProduct** pelo valor da coluna **ProductKey** e, em seguida, excluí-las, você pode mapear a coluna externa nomeada como **Param_0** para a coluna de entrada nomeada como **ProductKey** e, em seguida, executar a instrução SQL `DELETE FROM DimProduct WHERE ProductKey = ?`. A transformação Comando OLE DB fornece os nomes de parâmetro e você não pode modificá-los. Os nomes de parâmetro são **Param_0**, **Param_1**e assim por diante.  
  
 Se você configurar a transformação Comando OLE DB usando a caixa de diálogo **Editor Avançado** , os parâmetros na instrução SQL poderão ser mapeados automaticamente para colunas externas na entrada da transformação e as características de cada parâmetro poderão ser definidas, clicando no botão **Atualizar** . Entretanto, se o provedor OLE DB que a transformação Comando OLE DB usa não oferecer suporte para derivação de informações do parâmetro, você deverá configurar as colunas externas manualmente. Isto significa que você deve adicionar uma coluna para cada parâmetro na entrada externa para a transformação, atualizar os nomes de coluna para usar nomes como **Param_0**, especificar o valor da propriedade DBParamInfoFlags e mapear as colunas de entrada que contêm valores de parâmetro para as colunas externas.  
  
 O valor da propriedade DBParamInfoFlags representa as características do parâmetro. Por exemplo, o valor **1** especifica que o parâmetro é de entrada e o valor **65** especifica que o parâmetro é de entrada e pode conter um valor nulo. Os valores devem corresponder aos da enumeração OLE DB DBPARAMFLAGSENUM. Para obter mais informações, consulte a documentação de referência do OLE DB.  
  
 A transformação Comando OLE DB inclui a propriedade personalizada `SQLCommand`. Essa propriedade pode ser atualizada por uma expressão de propriedade quando o pacote é carregado. Para obter mais informações, consulte [Expressões do Integration Services &#40;SSIS&#41;](../../expressions/integration-services-ssis-expressions.md), [Usar expressões de propriedade em pacotes](../../expressions/use-property-expressions-in-packages.md) e [Propriedades personalizadas da transformação](transformation-custom-properties.md).  
  
 Essa transformação tem uma entrada, uma saída comum e uma saída de erro.  
  
## <a name="logging"></a>Registrando em log  
 Você poderá fazer log das chamadas que a transformação Comando OLE DB fizer a provedores de dados externos. Você pode usar esse recurso de log para solucionar problemas de conexões e comandos das fontes de dados externos executados pela transformação Comando OLE DB. Para fazer log das chamadas que a transformação Comando OLE DB fizer aos provedores de dados externos, habilite o log do pacote e selecione o evento **Diagnóstico** no nível de pacote. Para obter mais informações, consulte [Solucionando problemas de ferramentas para execução de pacotes](../../troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## <a name="related-tasks"></a>Related Tasks  
 Você pode configurar a transformação por meio do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer ou do modelo de objeto. Para obter detalhes sobre como configurar a transformação por meio do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer, consulte  [Configurar a transformação do Comando OLE DB](../../configure-the-ole-db-command-transformation.md). Consulte o Guia do Desenvolvedor para obter detalhes sobre como configurar essa transformação programaticamente.  
  
## <a name="see-also"></a>Consulte também  
 [Fluxo de Dados](../data-flow.md)   
 [Transformações do Integration Services](integration-services-transformations.md)  
  
  
