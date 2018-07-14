---
title: Opções de esquema de banco de dados de área (Assistente de geração de esquema) de assunto (Analysis Services - dados multidimensionais) | Microsoft Docs
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
- sql12.asvs.schemagenwizard.subjectareaschemaopts.f1
ms.assetid: 4c109bb8-e19d-412b-908f-bfdd7f872439
caps.latest.revision: 19
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: eb617bca3a906162f372ce482269d3fca386acec
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37235586"
---
# <a name="subject-area-database-schema-options-schema-generation-wizard-analysis-services---multidimensional-data"></a>Opções de Esquema de Banco de Dados da Área de Assunto (Assistente de Geração de Esquema) (Analysis Services - Dados Multidimensionais)
  Use a página **Opções de Esquema de Banco de Dados da Área de Assunto** para controlar como o esquema é gerado, bem como para definir como os dados são preservados.  
  
## <a name="options"></a>Opções  
 **Esquema de propriedade**  
 Especifica o nome do esquema dentro do banco de dados da nova área de assunto.  
  
 **Criar chaves primárias em tabelas de dimensão**  
 Cria chaves primárias nas tabelas de dimensões no esquema gerado. Nenhum índice será gerado se você não selecionar esta opção.  
  
> [!NOTE]  
>  Se você não selecionar esta opção, a integridade referencial será imposta.  
  
 **Criar índices**  
 Cria índices em colunas de chave estrangeira no esquema gerado.  
  
 **Impor a integridade referencial**  
 Impõe a integridade referencial dentro do esquema gerado. Se você não selecionar esta opção, relações serão criadas, mas não impostas.  
  
 **Preservar os dados na regeneração**  
 Retém dados no banco de dados de área de assunto quando o assistente é concluído. Se esta opção não for selecionada, todos os dados do banco de dados da área de assunto poderão ser apagados sem aviso prévio.  
  
 **Popular tabela (s) de tempo**  
 Especifica como o assistente popula as tabelas de tempo. A tabela a seguir descreve os possíveis valores para esta opção.  
  
> [!NOTE]  
>  Essa opção será habilitada apenas se o Assistente de Geração de Esquema for chamado no projeto do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] usando o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] no modo de projeto.  
  
|Valor|Description|  
|-----------|-----------------|  
|Popular|As tabelas de tempo de área de assunto são populadas.|  
|Não popular|As tabelas de tempo de área de assunto não são populadas.|  
|Popular somente se estiver vazia|As tabelas de tempo de área de assunto serão populadas apenas se estiverem vazias.|  
  
## <a name="see-also"></a>Consulte também  
 [Ajuda F1 do Assistente de geração de esquema &#40;Analysis Services - dados multidimensionais&#41;](schema-generation-wizard-f1-help-analysis-services-multidimensional-data.md)  
  
  
