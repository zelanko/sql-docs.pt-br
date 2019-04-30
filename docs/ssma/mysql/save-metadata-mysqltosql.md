---
title: Salvar metadados (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9bc6273f-e8b1-430b-81a5-14330a783562
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: f641b27357e75db0fb0f6ef71ff701d4f04b45a5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63154575"
---
# <a name="save-metadata--mysqltosql"></a>Salvar metadados (MySQLToSQL)
O **salvar metadados** caixa de diálogo solicita que você carregar metadados em seu projeto do SSMA antes de salvá-lo. Isso permite que você tiver um arquivo de projeto completo que você pode usar offline e enviar a outras pessoas, como a equipe de suporte técnico.  
  
Para acessar o **salvar metadados** caixa de diálogo, salve o projeto. Se todos os metadados estiverem ausentes, o SSMA exibirá os **salvar metadados** caixa de diálogo.  
  
## <a name="options"></a>Opções  
**Nome**  
O nome de cada banco de dados no projeto.  
  
**Status**  
Indica se os metadados são carregados para o projeto do SSMA, ou se os metadados estiverem ausentes.  
  
O SSMA carrega os metadados para o projeto conforme necessário. Metadados são carregados automaticamente quando você procurar os metadados e converter esquemas.  
  
**Selecionar Tudo**  
Seleciona listados todos os bancos de dados.  
  
**Liberada**  
Desmarca a caixa de seleção para todos os bancos de dados com metadados ausentes. Você não pode desmarcar a caixa de seleção se metadados tiver sido carregado.  
  
**Salvar**  
Salva o projeto, carregar os metadados para bancos de dados selecionados que têm metadados ausentes.  
  
**Cancelar**  
Cancela o salvamento operação. Metadados ausentes não é carregado no projeto.  
  
