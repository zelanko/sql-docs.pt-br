---
title: Configurar destino de arquivo simples (Assistente de Importação e Exportação do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.configureflatfiledest.f1
ms.assetid: 318e8da0-37d3-46cd-943a-fc5d66aad93a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 931c04a8a038612edcdaa48f40231c5fb6faed00
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48071486"
---
# <a name="configure-flat-file-destination-sql-server-import-and-export-wizard"></a>Configurar Destino Arquivo Simples (Assistente de Importação e Exportação do SQL Server)
  Use o **configurar destino arquivo simples** página para especificar opções de formatação para o arquivo simples de destino e visualizar os resultados antes de continuar.  
  
 Para saber mais sobre este assistente, consulte [SQL Server Import and Export Wizard](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Para saber mais sobre as opções para iniciar o assistente, bem como as permissões necessárias para executar o assistente com êxito, consulte [executar o Assistente de exportação e importação do SQL Server](start-the-sql-server-import-and-export-wizard.md).  
  
 O objetivo do Assistente de Importação e Exportação do SQL Server é copiar dados de uma origem para um destino. O assistente também pode criar um banco de dados de destino e tabelas de destino para você. No entanto, se for necessário copiar vários bancos de dados ou tabelas, ou outros tipos de objetos de banco de dados, será necessário usar o Assistente para Copiar Banco de Dados. Para obter mais informações, consulte [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="options"></a>Opções  
 **Arquivo simples de origem**  
 O nome do arquivo de destino.  
  
 **Delimitador de linha**  
 Selecione na lista de delimitadores para linhas.  
  
|Valor|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|A linha é delimitada por uma combinação de retorno de carro e avanço de linha.|  
|**{CR}**|A linha é delimitada por um retorno de carro.|  
|**{LF}**|A linha é delimitada por uma alimentação de linha.|  
|**Ponto-e-vírgula {;}**|A linha é delimitada por um ponto-e-vírgula.|  
|**Dois-pontos {:}**|A linha é delimitada por dois-pontos.|  
|**Vírgula {,}**|A linha é delimitada por uma vírgula.|  
|**Tabulação {t}**|A linha é delimitada por uma tabulação.|  
|**Barra vertical {&#124;}**|A linha é delimitada por uma barra vertical.|  
  
 **Delimitador de coluna**  
 Selecione na lista de delimitadores para colunas.  
  
|Valor|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|As colunas são delimitadas por um retorno de carro – linha combinação de alimentação.|  
|**{CR}**|As colunas são delimitadas por um retorno de carro.|  
|**{LF}**|As colunas são delimitadas por uma alimentação de linha.|  
|**Ponto-e-vírgula {;}**|As colunas são delimitadas por um ponto-e-vírgula.|  
|**Dois-pontos {:}**|As colunas são delimitadas por dois-pontos.|  
|**Vírgula {,}**|As colunas são delimitadas por uma vírgula.|  
|**Tabulação {t}**|As colunas são delimitadas por uma tabulação.|  
|**Barra vertical {&#124;}**|As colunas são delimitadas por uma barra vertical.|  
  
 **Visualização**  
 Exibir na **visualizar dados** caixa de diálogo Opções de resultados de formatação selecionadas para o arquivo simples de destino.  
  
 **Editar transformação**  
 Excluir linhas, acrescentar linhas e configurar colunas no arquivo de destino usando o **mapeamentos de coluna** caixa de diálogo.  
  
  
