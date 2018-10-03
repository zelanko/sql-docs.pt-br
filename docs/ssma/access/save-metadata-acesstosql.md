---
title: Salvar metadados (AcessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: fa4ce8ad-9935-4195-90f9-3fdac587a4ee
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: ff97098d021b3f9b566bcb4a336904940494676b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47673382"
---
# <a name="save-metadata-acesstosql"></a>Salvar metadados (AcessToSQL)
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
  
