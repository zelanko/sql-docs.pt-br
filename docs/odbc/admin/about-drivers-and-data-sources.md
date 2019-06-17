---
title: Sobre Drivers e fontes de dados | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 69516a613cbd9071686067350ced2ce5ca166a27
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63294449"
---
# <a name="about-drivers-and-data-sources"></a>Sobre drivers e fontes de dados
*Drivers* são os componentes que processam solicitações ODBC e retornam dados para o aplicativo. Se necessário, drivers de modificar uma solicitação de aplicativo em um formulário que é entendido pela fonte de dados. Você deve usar o programa de instalação do driver para adicionar ou excluir um driver do seu computador.  
  
 *Fontes de dados* são os bancos de dados ou arquivos acessados por um driver e são identificados por um nome de fonte de dados (DSN). Use o administrador de fonte de dados ODBC para adicionar, configurar e excluir fontes de dados do sistema. Os tipos de fontes de dados que podem ser usados são descritos na tabela a seguir.  
  
|Fonte de dados|Descrição|  
|-----------------|-----------------|  
|User|DSNs do usuário são locais para um computador e podem ser usados somente pelo usuário atual. Eles são registrados na subárvore do registro HKEY_CURRENT_USER.|  
|Sistema|DSNs de sistema são locais para um computador, em vez de dedicado a um usuário. O sistema ou qualquer usuário com privilégios pode usar uma fonte de dados configurada com um DSN de sistema. DSNs de sistema são registrados na subárvore do Registro HKEY_LOCAL_MACHINE.|  
|Arquivo|DSNs de arquivos são fontes com base em arquivo que podem ser compartilhados entre todos os usuários que têm os mesmos drivers instalados e, portanto, tem acesso ao banco de dados. Essas fontes de dados não precisam ser dedicadas a um usuário, nem ser local para um computador. Nomes de fonte de dados de arquivo não são identificados por entradas do registro dedicado; em vez disso, eles são identificados por um nome de arquivo com uma extensão. DSN.|  
  
 Fontes de dados de usuário e do sistema são coletivamente conhecidos como *machine* fontes de dados porque eles são locais para um computador.  
  
 Cada uma dessas fontes de dados tem uma guia **administrador de fonte de dados ODBC** caixa de diálogo. Para obter mais informações sobre as fontes de dados disponíveis, veja [Fontes de Dados](../../odbc/reference/data-sources.md).
