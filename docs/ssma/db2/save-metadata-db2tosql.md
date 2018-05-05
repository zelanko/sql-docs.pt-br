---
title: Salvar metadados (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-db2
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 9a76083e-4902-449e-b125-7e9259fc37f7
caps.latest.revision: 3
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: cd9b67c756c8153dcba9b94adc4333eb710f24bc
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="save-metadata-db2tosql"></a>Salvar metadados (DB2ToSQL)
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
  
