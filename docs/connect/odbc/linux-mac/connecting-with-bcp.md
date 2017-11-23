---
title: Conectando com bcp | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: bcp
ms.assetid: 3eca5717-e50f-40db-be16-a1cebbdfee70
caps.latest.revision: "33"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: f7e9db6a1ea636975a3f5719d9a1b3e9d5721eb6
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="connecting-with-bcp"></a>Conectando com bcp
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

O [bcp](http://go.microsoft.com/fwlink/?LinkID=190626) utilitário está disponível na [!INCLUDE[msCoName](../../../includes/msconame_md.md)] o Driver ODBC para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] em Linux e macOS. Esta página documenta as diferenças da versão do Windows `bcp`.
  
- O terminador de campo é um tab (“\t”).  
  
- O terminador de linha é um newline (“\n”).  
  
- Modo de caractere é o formato preferencial para `bcp` formatar arquivos e arquivos de dados que não contêm caracteres estendidos.  
  
> [!NOTE]  
> Uma barra invertida '\\' em um argumento de linha de comando deve ser entre aspas ou ignorado. Por exemplo, para especificar uma nova linha como um terminador de linha personalizado, você deve usar um dos seguintes mecanismos:  
>   
> -   -r\\\n  
> -   -r"\n"  
> -   -r'\n'  
  
A seguir está uma exemplo de invocação de comando `bcp` para copiar linhas da tabela para um arquivo de texto:  
  
```  
bcp AdventureWorks2008R2.Person.Address out test.dat -Usa -Pxxxx -Sxxx.xxx.xxx.xxx  
```  
  
## <a name="available-options"></a>Opções disponíveis
Na versão atual, a seguinte sintaxe e opções estão disponíveis:  

[*database***.**]*schema***.***table* **in** *data_file* | **out** *data_file*

- -a *packet_size*  
Especifica o número de bytes por pacote de rede enviado de e para o servidor.  
  
- -b *batch_size*  
Especifica o número de linhas por lote de dados importados.  
  
- -c  
Usa um tipo de dados de caractere  
  
- -d *database_name*  
Especifica o banco de dados que deve ser conectado.  
  
- -d  
Faz com que o valor passado para o `bcp` opção -S deve ser interpretado como um nome de fonte de dados (DSN). Para obter mais informações, consulte "Sn Support in sqlcmd e bcp" em [conectando com sqlcmd](../../../connect/odbc/linux-mac/connecting-with-sqlcmd.md).  
  
- -e *error_file* Especifica o caminho completo de um arquivo de erro usado para armazenar as linhas que o `bcp` utilitário não puder transferir do arquivo para o banco de dados.  
  
- -e  
Usa um valor ou valores de identidade no arquivo de dados importados para a coluna de identidade.  
  
- -f *format_file*  
Especifica o caminho completo de um arquivo de formato.  
  
- -f *first_row*  
Especifica o número da primeira linha que deve ser exportada de uma tabela ou importada de um arquivo de dados.  
  
- -k  
Especifica que colunas vazias devem reter um valor nulo durante a operação, em vez de qualquer valor padrão nas colunas inseridas.  
  
- -l  
Especifica um tempo limite de logon. A opção – l Especifica o número de segundos antes que um logon para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] o tempo limite ao tentar conectar a um servidor. O tempo de limite de logon padrão é 15 segundos. O tempo limite de logon deve ser um número entre 0 e 65534. O `bcp` irá gerar uma mensagem de erro se o valor fornecido não for numérico ou não estiver nesse intervalo. Um valor de 0 especifica um tempo limite infinito.
  
- -L *last_row*  
Especifica o número da última linha a ser exportada de uma tabela ou importada de um arquivo de dados.  
  
- -m *max_errors*  
Especifica o número máximo de erros de sintaxe que podem ocorrer antes do `bcp` operação foi cancelada.  
  
- -n  
Usa os tipos de dados nativos (do banco de dados) dos dados para realizar uma operação de cópia em massa.  
  
- -P *password*  
Especifica a senha para a ID de logon.  
  
- -Q  
Executa a instrução SET QUOTED_IDENTIFIERS ON na conexão entre o utilitário `bcp` e uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].  
  
- -r *row_terminator*  
Especifica o terminador de linha.  
  
- -r  
Especifica que dados de moeda, data e horário são copiados em massa no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] usando o formato regional definido para as configurações de localidade do computador cliente.  
  
- -S *server*  
Especifica o nome do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] instância a ser conectado, ou se -D for usado, um DSN.  
  
- -t *field_terminator*  
Especifica o terminador de campo.  
  
- -T  
Especifica que o `bcp` utilitário conectem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] com uma conexão confiável (segurança integrada).  
  
- -U *login_id*  
Especifica a ID de logon usada para conectar-se ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].  
  
- -v  
Informa o número de versão e copyright do utilitário `bcp`.  
  
- -w  
Executa a operação de cópia em massa usando caracteres Unicode.  
  
Nesta versão, há suporte para caracteres Latin-1 e UTF-16.  
  
## <a name="unavailable-options"></a>Opções indisponíveis
Na versão atual, a seguinte sintaxe e opções não estão disponíveis:  

- -c  
Especifica a página de código dos dados no arquivo de dados.  
  
- -h *hint*  
Especifica as dicas usadas durante uma importação de dados em massa para uma tabela ou exibição.  
  
- -i *input_file*  
Especifica o nome de um arquivo de resposta.  
  
- -n  
Usa os tipos de dados nativos (do banco de dados) dos dados para dados de não caractere e caracteres Unicode para dados de caractere.  
  
- -o *output_file*  
Especifica o nome de um arquivo que recebe a saída redirecionada do prompt de comando.  
  
- -V (80 | 90 | 100)  
Usa tipos de dados de uma versão anterior do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].  
  
- -x  
Usado com as opções format e -f format_file, gera um arquivo em formato baseado em XML, em vez do arquivo em formato não XML padrão.  
  
## <a name="see-also"></a>Consulte também

[Conectando com **sqlcmd**](../../../connect/odbc/linux-mac/connecting-with-sqlcmd.md)  
