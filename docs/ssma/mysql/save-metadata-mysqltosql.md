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
ms.openlocfilehash: 549c4b88e7ca75ce86c8a4e2ddd3eba25f138583
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67929366"
---
# <a name="save-metadata--mysqltosql"></a>Salvar metadados (MySQLToSQL)
A caixa de diálogo **salvar metadados** solicita que você carregue metadados em seu projeto do SSMA antes de salvá-lo. Isso permite que você tenha um arquivo de projeto completo que pode ser usado offline e enviado para outras pessoas, como a equipe de suporte técnico.  
  
Para acessar a caixa de diálogo **salvar metadados** , salve o projeto. Se algum metadado estiver ausente, o SSMA exibirá a caixa de diálogo **salvar metadados** .  
  
## <a name="options"></a>Opções  
**Nome**  
O nome de cada banco de dados no projeto.  
  
**Status**  
Indica se os metadados são carregados no projeto do SSMA ou se os metadados estão ausentes.  
  
O SSMA carrega metadados no projeto conforme necessário. Os metadados são carregados automaticamente quando você procura metadados e converte esquemas.  
  
**Selecionar Tudo**  
Seleciona todos os bancos de dados listados.  
  
**Formatação**  
Desmarca a caixa de seleção de todos os bancos de dados com metadados ausentes. Você não poderá desmarcar a caixa de seleção se um metadado tiver sido carregado.  
  
**Salvar**  
Salva o projeto, carregando metadados para os bancos de dados selecionados que têm metadados ausentes.  
  
**Cancelar**  
Cancela a operação de salvamento. Os metadados ausentes não são carregados no projeto.  
  
