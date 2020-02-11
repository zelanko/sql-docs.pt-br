---
title: Configurar destino de arquivo simples (Assistente de Importação e Exportação do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.configureflatfiledest.f1
ms.assetid: 318e8da0-37d3-46cd-943a-fc5d66aad93a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6504e4f5eee83d670b4843fb8d956b23a84d4aad
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62893027"
---
# <a name="configure-flat-file-destination-sql-server-import-and-export-wizard"></a>Configurar Destino Arquivo Simples (Assistente de Importação e Exportação do SQL Server)
  Use a página **Configurar destino de arquivo simples** para especificar opções de formatação para o arquivo simples de destino e para visualizar os resultados antes de continuar.  
  
 Para obter mais informações sobre este assistente, consulte [Assistente de Importação e Exportação do SQL Server](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Para saber mais sobre as opções de inicialização do assistente, bem como as permissões necessárias para executar o assistente com êxito, consulte [executar o assistente de importação e exportação do SQL Server](start-the-sql-server-import-and-export-wizard.md).  
  
 O objetivo do Assistente de Importação e Exportação do SQL Server é copiar dados de uma origem para um destino. O assistente também pode criar um banco de dados de destino e tabelas de destino para você. No entanto, se for necessário copiar vários bancos de dados ou tabelas, ou outros tipos de objetos de banco de dados, será necessário usar o Assistente para Copiar Banco de Dados. Para obter mais informações, consulte [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="options"></a>Opções  
 **Arquivo simples de origem**  
 O nome do arquivo de destino.  
  
 **Delimitador de linha**  
 Selecione na lista de delimitadores para linhas.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**CD ALIMENTAÇÃO**|A linha é delimitada por uma combinação de retorno de carro e avanço de linha.|  
|**CD**|A linha é delimitada por um retorno de carro.|  
|**ALIMENTAÇÃO**|A linha é delimitada por uma alimentação de linha.|  
|**Ponto e vírgula {;}**|A linha é delimitada por um ponto-e-vírgula.|  
|**Dois-pontos {:}**|A linha é delimitada por dois-pontos.|  
|**Pontos{,}**|A linha é delimitada por uma vírgula.|  
|**Guia {t}**|A linha é delimitada por uma tabulação.|  
|**Barra vertical {&#124;}**|A linha é delimitada por uma barra vertical.|  
  
 **Delimitador de coluna**  
 Selecione na lista de delimitadores para colunas.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**CD ALIMENTAÇÃO**|As colunas são delimitadas por uma combinação de retorno de carro e alimentação de linha.|  
|**CD**|As colunas são delimitadas por um retorno de carro.|  
|**ALIMENTAÇÃO**|As colunas são delimitadas por uma alimentação de linha.|  
|**Ponto e vírgula {;}**|As colunas são delimitadas por um ponto-e-vírgula.|  
|**Dois-pontos {:}**|As colunas são delimitadas por dois-pontos.|  
|**Pontos{,}**|As colunas são delimitadas por uma vírgula.|  
|**Guia {t}**|As colunas são delimitadas por uma tabulação.|  
|**Barra vertical {&#124;}**|As colunas são delimitadas por uma barra vertical.|  
  
 **Visualização**  
 Exibir na caixa de diálogo **Visualizar dados** os resultados das opções de formatação selecionadas para o arquivo simples de destino.  
  
 **Editar transformação**  
 Exclua linhas, acrescente linhas e configure colunas no arquivo de destino usando a caixa de diálogo **mapeamentos de coluna** .  
  
  
