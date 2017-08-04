---
title: Salvar metadados (OracleToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9e49c25f-9216-43f4-8e99-2eaab298e215
caps.latest.revision: 3
author: sabotta
ms.author: carlasab
manager: v-pelars
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 87e9060c8ca4de1b10d0522ce172581a8bcd88cf
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="save-metadata--oracletosql"></a>Salvar metadados (OracleToSQL)
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
  

