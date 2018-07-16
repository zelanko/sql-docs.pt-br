---
title: Configuração do servidor - agrupamento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- collation configuration, SQL Server
- collation configuration, Setup
- collation configuration
ms.assetid: e3986870-5be4-458b-b671-5ff12a27b022
caps.latest.revision: 19
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: abd57940e3caf8af66cb58fdeceebc802e877f6e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37290172"
---
# <a name="server-configuration---collation"></a>Configuração do SQL Server - Agrupamento
  Na página Configuração do Servidor - Agrupamento do Assistente de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , você pode modificar as configurações de agrupamento usadas pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)] e pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para fins de classificação. Selecione a opção para corresponder as configurações de agrupamento de instalações diferentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ou de outro computador.  
  
## <a name="options"></a>Opções  
 Personalizar para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece dois grupos de agrupamentos: agrupamentos do Windows e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agrupamentos. Você pode especificar configurações de agrupamento separadas para o [!INCLUDE[ssDE](../../includes/ssde-md.md)] e o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]ou especificar o mesmo agrupamento para ambos.  
  
 Por padrão, um agrupamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é selecionado para localidades do sistema do idioma inglês. O agrupamento padrão para versões localizadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é determinado pela configuração de localidade do sistema Windows em seu computador.  
  
 As configurações padrão devem ser alteradas apenas se a configuração de agrupamento dessa instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] corresponder às configurações de agrupamento usadas por outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ou se ela corresponder à localidade do sistema Windows de outro computador.  
  
 **Observação** [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa apenas agrupamentos do Windows. Se você planeja instalar o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], selecione um agrupamento do Windows durante o processo de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para garantir a consistência dos resultados entre o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Para obter mais informações, veja [Configurações de agrupamento na Instalação](http://go.microsoft.com/fwlink/?LinkId=190977).  
  
## <a name="best-practices"></a>Práticas recomendadas  
 Para obter mais informações sobre uma tabela de localidades de Sistema do Windows e os agrupamentos padrão correspondentes usados pela Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , veja [Configurações de agrupamento na Instalação](http://go.microsoft.com/fwlink/?LinkId=190977).  
  
 Se possível, use um agrupamento exclusivo para sua organização. Dessa forma, não será preciso especificar explicitamente o agrupamento para cada banco de dados, coluna, expressão ou identificador. Se você precisar trabalhar com vários agrupamentos e configurações de página de códigos diferentes, codifique suas consultas para considerar as regras da precedência de agrupamento. Para obter mais informações, confira o tópico [Precedência de agrupamento &#40;Transact-SQL&#41;](/sql/t-sql/statements/collation-precedence-transact-sql) nos Manuais Online.  
  
 Quando você selecionar um agrupamento para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], considere as seguintes recomendações:  
  
-   Selecione um agrupamento BINARY2 se ordenação binária baseada em ponto de código for aceitável.  
  
-   Selecione um agrupamento do Windows para que a comparação seja consistente em todos os tipos de dados.  
  
-   Use um novo agrupamento nível 100 para obter um suporte melhor à classificação lingüística. Para obter mais informações, consulte [Suporte a agrupamentos e Unicode](../../relational-databases/collations/collation-and-unicode-support.md).  
  
-   Caso você pretenda migrar um banco de dados para a instância atualizada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], selecione o agrupamento correspondente ao seu agrupamento existente do banco de dados.  
  
  
