package application;

import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class Program {
	public static void main(String[] args) {
		
		List<String> list = new ArrayList<>();
		String path = "C:\\Projetos\\in.txt";
		
		try (BufferedReader br = new BufferedReader(new FileReader(path))) {
			
			String name = br.readLine();
			while (name != null) {
				list.add(name);
				name = br.readLine();
			}
			/*
			 * Depois eu vou chamar essa operação aqui da classe collections, collections.sort, passando a minha lista
			 * como argumento. Essa operação aqui é uma operação padrão, é uma forma de você ordenar uma coleção, feito 
			 * isso eu vou ter minha lista ordenada, eu vou percorrer a minha lista usando for each imprimindo cada um
			 * dos elementos.
			 */
			Collections.sort(list);
			for (String s : list) {
				System.out.println(s);
			}
			
		} catch (IOException e) {
			System.out.println("Error: " + e.getMessage());
		}
	}
}
