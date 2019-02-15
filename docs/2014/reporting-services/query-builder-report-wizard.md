---
title: (Assistente de relatório) do construtor de consultas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.dataview.vdtquerydesigner.f1
- sql12.rtp.rptwizard.querybuilder.f1
helpviewer_keywords:
- Query Builder [Reporting Services]
ms.assetid: 1b0904ea-28c1-448e-b56c-c0fdfbc8b222
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 358a82555a2f0b3df8a7635cb3ff39a7b09f2e50
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56290394"
---
# <a name="query-builder-report-wizard"></a>Construtor de Consultas (Assistente de Relatório)
  Use o Construtor de Consultas para especificar uma consulta que recupera um conjunto de resultados para usar em um relatório. Você pode escolher entre dois construtores de consulta:  
  
-   O construtor de consultas baseado em texto (padrão) fornece um workspace simples para especificar uma consulta e exibir os resultados. Você pode especificar várias instruções do [!INCLUDE[tsql](../includes/tsql-md.md)] , consulta ou sintaxe de comando para as extensões de processamento de dados e consultas que são especificadas como expressões. Como o construtor de consulta genérico não processa previamente a consulta e pode acomodar qualquer tipo de sintaxe de consulta, esta é a ferramenta de construção de consulta padrão para o Designer de Relatórios.  
  
-   O construtor de consultas gráfico fornece uma experiência visual mais rica. É usado no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] e em outras partes do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Você poderá usar o construtor de consultas gráfico se não estiver criando expressões ou instruções SQL de várias partes.  
  
     Para mudar para o construtor de consultas gráfico, ative/desative o botão **Editar como Texto** , no canto superior esquerdo da janela.  
  
 Você também pode importar uma consulta de outro relatório.  
  
## <a name="query-builder-options"></a>Opções do Construtor de Consultas  
 **Editar como Texto**  
 Alterna entre os designers de consultas gráficas e baseados em texto, se ambos funcionarem para a consulta.  
  
 **Importar**  
 Abre a caixa de diálogo **Importar Consulta** e exibe arquivos .rdl e .sql de qualquer relatório disponível. Você pode usar a consulta importada como ela está ou pode modificá-la no construtor de consultas.  
  
 **! (Run)**  
 Executa a consulta e retorna um conjunto de resultados se a consulta for válida. Observe que você não poderá executar a consulta se ela for uma expressão. Para verificar uma consulta baseada em expressão, você deve visualizar o relatório.  
  
 **Tipo de comando**  
 Especifica o direcionamento de texto, o procedimento armazenado ou a tabela. A disponibilidade de um tipo de comando depende da extensão de processamento de dados que você especificou.  
  
 **Painel de consulta**  
 Digite a consulta.  
  
 **Painel de resultados**  
 Mostra o conjunto de resultados retornado da consulta.  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [Ajuda do Assistente de Relatório](../../2014/reporting-services/report-wizard-help.md)  
  
  
