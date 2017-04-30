# MyHomework
package exercise2;

import java.io.*;


public class Serch {
	public long countAllNum(File file){
		long count = 0;
		if(file.isFile()){
			if(file.getName().endsWith(".java")){
				System.out.print(file.getName());
				count = countLineNum(file);
				System.out.println(count);
			}

		}else if(file.isDirectory()){
			File[] fs = file.listFiles();
			for(File temp: fs){
				count+=countAllNum(temp);
			}
		}
		return count;
	}
	public long countLineNum(File file){
		long sum = 0;
		try {
			BufferedReader br = new BufferedReader(new FileReader(file));
			String line = null;
			while((line = br.readLine()) != null){
				sum += countNum(line);
			}
			br.close();
		} catch (Exception e) {
			e.printStackTrace();
		}
		return sum;
	}
	public long countNum(String line){
		long num = 0;
		String[] s = line.replaceAll("[^0-9]", ",").split(",");
		for(String temp:s){
			if(temp.length() > 0){
				num += Integer.parseInt(temp);
			}
		}
		return num;
	}
}
