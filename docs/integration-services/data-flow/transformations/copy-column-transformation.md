---
title: Copiar Transformação de Coluna | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.copycolumntrans.f1
- sql13.dts.designer.copymaptransformation.f1
helpviewer_keywords:
- columns [Integration Services], copying
- copying columns
- Copy Column transformation
ms.assetid: 1c72a313-9026-46bc-a57f-c6b3f47346f8
caps.latest.revision: 37
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 030d3ec6f764222533cca1d9b6569eb2969c454e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="copy-column-transformation"></a>transformação Copiar Coluna
  A transformação Copiar Coluna cria novas colunas com a cópia de colunas de entrada e a adição de novas colunas à saída da transformação. Mais tarde no fluxo de dados, transformações diferentes podem ser aplicadas às cópias da coluna. Por exemplo, você pode usar a transformação Copiar Coluna para criar uma cópia de uma coluna e, em seguida, converter os dados copiados em caracteres maiúsculos por meio da transformação Mapa de Caracteres ou aplicar agregações à coluna nova por meio da transformação Agregação.  
  
## <a name="configuration-of-the-copy-column-transformation"></a>Configuração da transformação Copiar Coluna  
 Configure a transformação Copiar Coluna especificando as colunas de entrada a serem copiadas. É possível criar várias cópias de uma coluna ou criar cópias de várias colunas em uma operação.  
  
 Essa transformação tem uma entrada e uma saída. Não dá suporte a uma saída de erro.  
  
 Você pode definir propriedades por meio do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer ou programaticamente.  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propriedades personalizadas de Transformação](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Para obter mais informações sobre como definir as propriedades, consulte [Definir as propriedades de um componente de fluxo de dados](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="copy-column-transformation-editor"></a>Editor de Transformação Copiar Coluna
  Use a caixa de diálogo **Editor de Transformação Copiar Coluna** para selecionar colunas para copiar e nomear as novas colunas de saída.  
  
> [!NOTE]  
>  Ao copiar apenas todos os dados de origem para um destino, poderá não ser necessário usar a transformação Copiar Coluna. Em alguns cenários, você pode conectar uma origem diretamente para um destino, quando nenhuma transformação de dados é requerida. Nestas circunstâncias é frequentemente preferível usar o Assistente de Importação e Exportação do SQL Server para criar o pacote para você. Depois você pode aprimorar e reconfigurar o pacote conforme a necessidade. Para obter mais informações, consulte [SQL Server Import and Export Wizard](~/integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md).  
  
### <a name="options"></a>Opções  
 **Colunas de Entrada Disponíveis**  
 Selecione as colunas para copiar, usando as caixas de seleção. as seleções adicionam colunas de entrada à tabela abaixo.  
  
 **Coluna de Entrada**  
 Selecione colunas para copiar na lista de colunas de entrada disponíveis. As seleções se refletem naquelas da caixa de seleção da tabela **Colunas de Entrada Disponíveis** .  
  
 **Alias de Saída**  
 Digite um alias para cada nova coluna de saída. O padrão é **Copiar de**, seguido do nome da coluna de entrada; no entanto, é possível escolher qualquer nome descritivo exclusivo.  
  
## <a name="see-also"></a>Consulte Também  
 [Fluxo de Dados](../../../integration-services/data-flow/data-flow.md)   
 [Transformações do Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
