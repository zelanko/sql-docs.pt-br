---
title: Configuração do servidor - agrupamento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- collation configuration, SQL Server
- collation configuration, Setup
- collation configuration
ms.assetid: e3986870-5be4-458b-b671-5ff12a27b022
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: dbc80b6f50ea023a998b6a7958577933afd007a7
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53362339"
---
# <a name="server-configuration---collation"></a>Configuração do SQL Server – ordenação
  Na página Configuração do Servidor - Ordenação do Assistente de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você pode modificar as configurações de ordenação usadas pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)] e pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para fins de classificação. Selecione a opção para corresponder as configurações de ordenação de instalações diferentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou de outro computador.  
  
## <a name="options"></a>Opções  
 Personalizar para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece dois grupos de agrupamentos: Agrupamentos do Windows e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agrupamentos. Você pode especificar configurações de ordenação separadas para o [!INCLUDE[ssDE](../../includes/ssde-md.md)] e o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou especificar a mesma ordenação para ambos.  
  
 Por padrão, uma ordenação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é selecionada para localidades do sistema do idioma inglês. A ordenação padrão para versões localizadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é determinada pela configuração de localidade do sistema Windows em seu computador.  
  
 As configurações padrão devem ser alteradas apenas se a configuração de ordenação dessa instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] corresponder às configurações de ordenação usadas por outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou se ela corresponder à localidade do sistema Windows de outro computador.  
  
 **Observação**[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa apenas ordenações do Windows. Se você planeja instalar o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], selecione uma ordenação do Windows durante o processo de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para garantir a consistência dos resultados entre o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Para obter mais informações, veja [Configurações de ordenação na Instalação](https://go.microsoft.com/fwlink/?LinkId=190977).  
  
## <a name="best-practices"></a>Práticas recomendadas  
 Para obter mais informações sobre uma tabela de localidades de Sistema do Windows e as ordenações padrão correspondentes usadas pela Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], veja [Configurações de ordenação na Instalação](https://go.microsoft.com/fwlink/?LinkId=190977).  
  
 Se possível, use uma ordenação exclusiva para sua organização. Dessa forma, não será preciso especificar explicitamente a ordenação para cada banco de dados, coluna, expressão ou identificador. Se você precisar trabalhar com várias ordenações e configurações de página de códigos diferentes, codifique suas consultas para considerar as regras da precedência de ordenação. Para obter mais informações, confira o tópico [Precedência de ordenação &amp;#40;Transact-SQL&amp;#41;](/sql/t-sql/statements/collation-precedence-transact-sql) nos Manuais Online.  
  
 Quando você selecionar uma ordenação para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], considere as seguintes recomendações:  
  
-   Selecione uma ordenação BINARY2 se ordenação binária baseada em ponto de código for aceitável.  
  
-   Selecione uma ordenação do Windows para que a comparação seja consistente em todos os tipos de dados.  
  
-   Use uma nova ordenação nível 100 para obter um suporte melhor à classificação lingüística. Para obter mais informações, consulte [Suporte a agrupamentos e Unicode](../../relational-databases/collations/collation-and-unicode-support.md).  
  
-   Caso você pretenda migrar um banco de dados para a instância atualizada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], selecione a ordenação correspondente à sua ordenação existente do banco de dados.  
  
  
