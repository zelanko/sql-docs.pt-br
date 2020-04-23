---
title: 'Etapa 1: Configurar o ambiente para PHP'
description: A etapa 1 deste guia de introdução envolve a instalação do PHP, do Microsoft ODBC Driver for SQL Server e a configuração do seu ambiente de desenvolvimento.
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 0bce6022-00bd-45c6-9671-eaa9dfa395a8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 88eb2c2c67eac3ecd9fba2c79c143de28cf60d22
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81633167"
---
# <a name="step-1-configure-environment-for-php-development"></a>Etapa 1: Configurar o ambiente para o desenvolvimento em PHP
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]




* Com base em seu ambiente, identifique qual versão do Driver PHP você usará, conforme observado aqui:  [Requisitos do sistema para os Microsoft Drivers for PHP for SQL Server](system-requirements-for-the-php-sql-driver.md)
* Baixe e instale o Driver PHP aplicável aqui: [Baixar o Microsoft PHP Driver](https://www.microsoft.com/download/details.aspx?id=20098)  
* Baixe e instale o Driver ODBC aplicável aqui:  [Baixar o driver ODBC para SQL Server](../odbc/download-odbc-driver-for-sql-server.md)  
* Configure o driver PHP e o servidor Web para seu sistema operacional específico:

### <a name="windows"></a>Windows  
  

* Configure o carregamento do driver PHP, conforme observado aqui: [Carregando os Microsoft Drivers for PHP for SQL Server](../../connect/php/loading-the-php-sql-driver.md) 
* Configure o IIS para hospedar aplicativos PHP, conforme observado aqui: [Configuração do IIS para os drivers da Microsoft para PHP para SQL Server](../../connect/php/configuring-iis-for-php-sql-driver.md)

### <a name="linux-and-macos"></a>Linux e macOS


*   Configure o carregamento do driver PHP e configure seu servidor Web para hospedar aplicativos PHP, conforme observado aqui: [Tutorial de Instalação de Drivers PHP de Linux e de macOS](../../connect/php/installation-tutorial-linux-mac.md)
