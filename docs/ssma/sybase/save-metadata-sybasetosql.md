---
title: Salvar metadados (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: b2517735-dd19-449f-8cee-08e68ca89d3a
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 3a8cde296fd0a47c407752977f5e41269a05354e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68020972"
---
# <a name="save-metadata--sybasetosql"></a>Salvar metadados (SybaseToSQL)
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
  
