---
title: Recuperação de dados como um fluxo usando o driver SQLSRV | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 17dc9129-04cd-430c-b5b3-82824116425d
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d5d1d7e62709af773ca251a389c8cfaa4981ce58
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66797051"
---
# <a name="retrieving-data-as-a-stream-using-the-sqlsrv-driver"></a>Recuperando dados como um fluxo usando o driver SQLSRV
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

A recuperação de dados como um fluxo só está disponível no driver SQLSRV dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], e não está disponível no driver PDO_SQLSRV.  
  
Os [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] aproveitam os fluxos para recuperar grandes quantidades de dados. Os tópicos nesta seção fornecem detalhes sobre como recuperar dados como um fluxo.  
  
As etapas a seguir resumem como recuperar dados como um fluxo:  
  
1.  Preparar e executar uma consulta Transact-SQL com [sqlsrv_query](../../connect/php/sqlsrv-query.md) ou uma combinação de [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)/[sqlsrv_execute](../../connect/php/sqlsrv-execute.md).  
  
2.  Use [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md) para passar para a próxima linha no conjunto de resultados.  
  
3.  Use [sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md) para recuperar um campo da linha. Especifique que os dados devem ser recuperados como um fluxo usando **SQLSRV_PHPTYPE_STREAM(<encoding>)** como o terceiro parâmetro na chamada de função. Esta tabela lista as constantes usadas para especificar as codificações e suas descrições:  
  
    |Constante SQLSRV|Descrição|  
    |-------------------|---------------|  
    |SQLSRV_ENC_BINARY|Os dados são retornados do servidor como um fluxo de bytes brutos, sem codificação ou conversão.|  
    |SQLSRV_ENC_CHAR|Os dados são retornados em caracteres de 8 bits conforme especificado na página de código da localidade do Windows definida no sistema. Todos os caracteres multibyte ou caracteres não mapeados nessa página de código são substituídos por um caractere de ponto de interrogação (?) de byte único.|  
  
> [!NOTE]  
> Por padrão, alguns tipos de dados são retornados como fluxos. Para obter mais informações, consulte [Default PHP Data Types](../../connect/php/default-php-data-types.md).  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Descrição|  
|---------|---------------|  
|[Tipos de dados com suporte a fluxo usando o driver SQLSRV](../../connect/php/data-types-with-stream-support-using-the-sqlsrv-driver.md)|Lista os tipos de dados do SQL Server que podem ser recuperados como fluxos.|  
|[Como recuperar dados de caractere como um fluxo usando o driver SQLSRV](../../connect/php/how-to-retrieve-character-data-as-a-stream-using-the-sqlsrv-driver.md)|Demonstra como recuperar dados de caractere como um fluxo.|  
|[Como recuperar dados binários como um fluxo usando o driver SQLSRV](../../connect/php/how-to-retrieve-binary-data-as-a-stream-using-the-sqlsrv-driver.md)|Demonstra como recuperar dados binários como um fluxo.|  
  
## <a name="see-also"></a>Consulte Também  
[Recuperando dados](../../connect/php/retrieving-data.md)

[Constantes &#40;Drivers da Microsoft para PHP para SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
  
