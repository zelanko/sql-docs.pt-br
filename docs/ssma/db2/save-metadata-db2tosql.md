---
description: Salvar metadados (DB2ToSQL)
title: Salvar metadados (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9a76083e-4902-449e-b125-7e9259fc37f7
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 0a8972f267c21fdd43b01a7316ddd199400733de
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88463458"
---
# <a name="save-metadata-db2tosql"></a>Salvar metadados (DB2ToSQL)
A caixa de diálogo **salvar metadados** solicita que você carregue metadados em seu projeto do SSMA antes de salvá-lo. Isso permite que você tenha um arquivo de projeto completo que pode ser usado offline e enviado para outras pessoas, como a equipe de suporte técnico.  
  
Para acessar a caixa de diálogo **salvar metadados** , salve o projeto. Se algum metadado estiver ausente, o SSMA exibirá a caixa de diálogo **salvar metadados** .  
  
## <a name="options"></a>Opções  
**Nome**  
O nome de cada banco de dados no projeto.  
  
**Status**  
Indica se os metadados são carregados no projeto do SSMA ou se os metadados estão ausentes.  
  
O SSMA carrega metadados no projeto conforme necessário. Os metadados são carregados automaticamente quando você procura metadados e converte esquemas.  
  
**Selecionar tudo**  
Seleciona todos os bancos de dados listados.  
  
**Limpar**  
Desmarca a caixa de seleção de todos os bancos de dados com metadados ausentes. Você não poderá desmarcar a caixa de seleção se um metadado tiver sido carregado.  
  
**Salvar**  
Salva o projeto, carregando metadados para os bancos de dados selecionados que têm metadados ausentes.  
  
**Cancelar**  
Cancela a operação de salvamento. Os metadados ausentes não são carregados no projeto.  
  
