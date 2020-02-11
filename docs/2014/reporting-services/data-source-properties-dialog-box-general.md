---
title: Caixa de diálogo Propriedades da fonte de dados, geral | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.datasourceproperties.general.f1
- "10120"
ms.assetid: 44b5edd3-5c11-4d3d-91b8-5871aa0572ed
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9f918d6583f01473e061792406821b13a4856cea
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66109482"
---
# <a name="data-source-properties-dialog-box-general"></a>Caixa de diálogo Propriedades da Fonte de Dados, Geral
  Selecione **Geral** na caixa de diálogo **Propriedades da Fonte de Dados** para exibir e modificar as informações de conexão para a fonte de dados no relatório.  
  
## <a name="options"></a>Opções  
 **Nome**  
 Digite o nome da fonte de dados. O nome da fonte de dados deve ser exclusivo no relatório. Por padrão, um nome geral, como DataSource1 ou DataSource2, é atribuído à fonte de dados.  
  
 **Conexão inserida**  
 Selecione esta opção quando você não quiser usar uma fonte de dados compartilhada.  
  
 **Tipo**  
 Selecione uma extensão de processamento de dados. A lista exibe todas as extensões registradas.  
  
 **Cadeia de conexão**  
 Informe uma cadeia de conexão para a fonte de dados. Clique em **Editar** para criar a cadeia de conexão usando a caixa de diálogo **Propriedades da Conexão** . Clique no botão **Expressões** (*fx*) para editar a expressão.  
  
 **Usar referência da fonte de dados compartilhada**  
 Selecione esta opção para estabelecer um vínculo com uma fonte de dados compartilhada. Selecione uma fonte de dados compartilhada da lista suspensa. Para editar a fonte de dados selecionada, clique em **Editar**. Se a opção **Usar referência da fonte de dados compartilhada** estiver selecionada, as opções **Tipo** e **Cadeia de Conexão** serão desabilitadas.  
  
 **Usar uma única transação ao processar as consultas**  
 Selecione esta opção para indicar que os conjuntos de dados que usam essa fonte de dados serão executados em uma única transação no banco de dados. Para incluir as transações de sub-relatórios que usam a mesma fonte de dados, defina **MergeTransactions** como **True** na seção de propriedades **Outros** do sub-relatório do painel **Propriedades** .  
  
## <a name="see-also"></a>Consulte Também  
 [Adicionar dados a um relatório &#40;Construtor de Relatórios e SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [Criar uma fonte de dados inserida ou compartilhada &#40;SSRS&#41;](../../2014/reporting-services/create-an-embedded-or-shared-data-source-ssrs.md)   
 [Conexões de dados, fontes de dados e cadeias de conexão no Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Caixa de diálogo Propriedades da Fonte de Dados, Credenciais](../../2014/reporting-services/data-source-properties-dialog-box-credentials.md)  
  
  
