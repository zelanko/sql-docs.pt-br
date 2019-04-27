---
title: Exibir o esquema do cubo | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 93898e6ed8dc26e3b06fd6a583bfa4084dd4c5f2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62740686"
---
# <a name="view-the-cube-schema"></a>Exibir o esquema do cubo
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  O painel **Exibição da Fonte de Dados** da guia **Estrutura do Cubo** no **Designer do Cubo** exibe o esquema do cubo. O esquema é o conjunto de tabelas das quais são derivadas as medidas e as dimensões para um cubo. Todo esquema de cubo consiste em uma ou mais tabelas de fato e uma ou mais tabelas de dimensão nas quais são baseadas as medidas e as dimensões no cubo.  
  
 O painel **Exibição da Fonte de Dados** da guia **Estrutura do Cubo** exibe um diagrama da exibição da fonte de dados na qual o cubo está baseado. Este diagrama é um subconjunto do diagrama principal da exibição da fonte de dados. Você pode ocultar e mostrar tabelas no painel **Exibição da Fonte de Dados** e exibir qualquer diagrama existente. Porém, você não pode fazer alterações (como adicionar novas relações ou consultas nomeadas) ao esquema subjacente. Para fazer alterações ao esquema, use o Designer de Exibição da Fonte de Dados.  
  
 Quando você cria um cubo, o diagrama exibido no painel **Exibição da fonte de dados** da guia **Estrutura do Cubo** é inicialmente igual ao diagrama **Mostrar Todas as Tabelas** na exibição da fonte de dados para o projeto ou banco de dados. Você pode substituir o diagrama por qualquer diagrama existente na exibição da fonte de dados e fazer ajustes no painel **Exibição da Fonte de Dados** .  
  
 Enquanto você trabalha com o diagrama no **Designer do Cubo**, comandos que agem na guia ou em algum objeto selecionado na guia estão disponíveis no menu **Exibição da Fonte de Dados** . Você também pode clicar com o botão direito no plano de fundo do diagrama ou qualquer objeto no diagrama para usar comandos que agem no diagrama ou objeto selecionado. Você pode:  
  
-   Alternar entre diagrama e formatos de árvore.  
  
-   Organizar, localizar, mostrar e ocultar tabelas.  
  
-   Mostrar Nomes Amigáveis.  
  
-   Alternar layouts.  
  
-   Alterar a ampliação.  
  
-   Exibir propriedades.  
  
 Adicionalmente, você pode executar as ações listadas na tabela a seguir:  
  
|Para|Faça isto|  
|--------|-------------|  
|Use um diagrama da exibição da fonte de dados do cubo|No menu **Exibição da Fonte de Dados** , aponte para **Copiar Diagrama de**e clique no diagrama da exibição da fonte de dados que você deseja usar.<br /><br /> - ou -<br /><br /> Clique com o botão direito do mouse na tela de fundo do painel **Exibição da Fonte de Dados** , aponte para **Copiar Diagrama de**e clique no diagrama na exibição da fonte de dados que você deseja usar. Este método cria uma cópia independente do diagrama, de modo que qualquer alteração que você faz na guia **Construtor de Cubos** não aparece no diagrama original.|  
|Mostrar somente as tabelas que são usadas no cubo|No menu **Exibição da Fonte de Dados** , clique em **Mostrar Somente Tabelas Usadas**.<br /><br /> - ou -<br /><br /> Clique com o botão direito do mouse na tela de fundo do painel **Exibição da Fonte de Dados** e clique em **Mostrar Somente Tabelas Usadas**.|  
|Editar o esquema da exibição da fonte de dados|No menu **Exibição da Fonte de Dados** , clique em **Editar Exibição da Fonte de Dados**.<br /><br /> - ou -<br /><br /> Clique com o botão direito do mouse na tela de fundo do painel **Exibição da Fonte de Dados** e clique em **Editar Exibição da Fonte de Dados**.|  
  
  
