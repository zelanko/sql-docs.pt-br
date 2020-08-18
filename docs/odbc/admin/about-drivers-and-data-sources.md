---
description: Sobre drivers e fontes de dados
title: Sobre drivers e fontes de dados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC data source administrator [ODBC], concepts
ms.assetid: 2bb83ef1-4bbe-4be3-8c32-c4d1140aae1d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 141a8e99a219923fa8e658c2600e79cad6f4ae93
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386582"
---
# <a name="about-drivers-and-data-sources"></a>Sobre drivers e fontes de dados
Os *drivers* são os componentes que processam solicitações ODBC e retornam dados para o aplicativo. Se necessário, os drivers modificam a solicitação de um aplicativo em um formulário compreendido pela fonte de dados. Você deve usar o programa de instalação do driver para adicionar ou excluir um driver do seu computador.  
  
 As *fontes de dados* são os bancos ou os arquivos acessados por um driver e são identificados por um DSN (nome da fonte de dados). Use o administrador de fonte de dados ODBC para adicionar, configurar e excluir fontes de dados do seu sistema. Os tipos de fontes de dados que podem ser usados são descritos na tabela a seguir.  
  
|Fonte de dados|Descrição|  
|-----------------|-----------------|  
|Usuário|Os DSNs de usuário são locais para um computador e podem ser usados somente pelo usuário atual. Eles são registrados na subárvore do registro HKEY_CURRENT_USER.|  
|Sistema|Os DSNs do sistema são locais para um computador em vez de dedicados a um usuário. O sistema ou qualquer usuário com privilégios pode usar uma fonte de dados configurada com um DSN do sistema. Os DSNs do sistema são registrados na subárvore do registro do HKEY_LOCAL_MACHINE.|  
|Arquivo|Os DSNs de arquivo são fontes baseadas em arquivo que podem ser compartilhadas entre todos os usuários que têm os mesmos drivers instalados e, portanto, têm acesso ao banco de dados. Essas fontes de dados não precisam ser dedicadas a um usuário nem ser locais para um computador. Nomes de fonte de dados de arquivo não são identificados por entradas de registro dedicadas; em vez disso, eles são identificados por um nome de arquivo com uma extensão. DSN.|  
  
 As fontes de dados do usuário e do sistema são coletivamente conhecidas como fontes de dados do *computador* porque são locais para um computador.  
  
 Cada uma dessas fontes de dados tem uma guia na caixa de diálogo **administrador de fonte de dados ODBC** . Para obter mais informações sobre as fontes de dados disponíveis, veja [Fontes de Dados](../../odbc/reference/data-sources.md).
