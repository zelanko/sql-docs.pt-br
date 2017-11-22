---
title: Salvar metadados (MySQLToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 9bc6273f-e8b1-430b-81a5-14330a783562
caps.latest.revision: "3"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6515e7747aa5137849acab0bfc3540d3ecc59996
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="save-metadata--mysqltosql"></a>Salvar metadados (MySQLToSQL)
O **salvar metadados** caixa de diálogo solicita que você carregar metadados em seu projeto SSMA antes de salvá-lo. Isso permite que você tem um arquivo de projeto completo que você pode usar offline e enviar a outras pessoas, como a equipe de suporte técnico.  
  
Para acessar o **salvar metadados** caixa de diálogo, salve o projeto. Se todos os metadados estiverem ausentes, o SSMA exibirá o **salvar metadados** caixa de diálogo.  
  
## <a name="options"></a>Opções  
**Nome**  
O nome de cada banco de dados no projeto.  
  
**Status**  
Indica se metadados forem carregados no projeto SSMA, ou se os metadados estão faltando.  
  
O SSMA carrega os metadados no projeto conforme necessário. Metadados é carregado automaticamente quando você procura os metadados e converter esquemas.  
  
**Selecionar Tudo**  
Seleciona todos os listados bancos de dados.  
  
**Liberada**  
Limpa a caixa de seleção para todos os bancos de dados com metadados ausentes. Você não pode desmarcar a caixa de seleção se metadados forem carregado.  
  
**Salvar**  
Salva o projeto, carregar os metadados para bancos de dados selecionados que possuem metadados ausentes.  
  
**Cancelar**  
Cancela o salvamento operação. Faltando metadados não é carregado no projeto.  
  
