---
title: Opções (página Editor de texto – XML – diversos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 1a9509f0-c663-4b31-b396-7f5dc4371651
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: eb3422b859ce4e58fc05564357876c5fe09fcdff
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66089205"
---
# <a name="options-text-editor---xml---miscellaneous-page"></a>Opções (página Editor de texto – XML – Diversos)

A caixa de diálogo **Opções** permite alteração das configurações de preenchimento automático e de esquema para o Editor de XML. Essas configurações estão disponíveis quando, no menu **Ferramentas** , você clica em **Opções**expande a pasta **Editor de Texto** , clica em **XML** e, então, clica em **Diversos** .  
  
## <a name="auto-insert"></a>Inserir automaticamente  
 **Fechar marcas**  
 O Editor de Texto adiciona marcas íntimas ao criar elementos XML. Se uma marca de início de elemento for selecionada, o editor insere a marca íntima correspondente, incluindo um prefixo de namespace correspondente. Esta caixa de seleção fica marcada por padrão.  
  
 **Citações de atributo**  
 Ao criar atributos XML, o editor insere os caracteres `="``"` e coloca o sinal de inclusão (**^)** entre aspas. Esta caixa de seleção fica marcada por padrão.  
  
 **Declarações de namespace**  
 O editor insere declarações de namespace automaticamente onde quer elas sejam necessárias. Esta caixa de seleção fica marcada por padrão.  
  
 **Outra remarcação (Comentários, CDATA)**  
 Comentários, CDATA, DOCTYPE, instruções de processamento e outra remarcação e autocompletada. Esta caixa de seleção fica marcada por padrão.  
  
## <a name="network"></a>Rede  
 **Carregar automaticamente DTDs e esquemas**  
 Esquemas e DTDs (definições de tipo de documento) são baixados automaticamente de locais HTTP. Esse recurso usa System.Net com detecção de servidor de autoproxy habilitada. Esta caixa de seleção fica marcada por padrão.  
  
## <a name="outlining"></a>Estrutura de tópicos  
 **Entrar no modo de estrutura de tópicos quando os arquivos forem abertos**  
 Ativa o recurso de estrutura de tópicos quando um arquivo é aberto. Esta caixa de seleção fica marcada por padrão.  
  
## <a name="caching"></a>Cache  
 **Esquemas**  
 Especifica o local do cache de esquema. O botão Procurar (...) abre o local d cache de esquema atual em uma janela nova. O local padrão é * \<Management Studio diretório de instalação>* \Xml\Schemas.  
