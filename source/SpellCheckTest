import java.util.ArrayList;
import java.util.Collections;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
import java.util.Set;
import java.util.HashSet;


public class SpellChecker {
	private Map<String, Integer> mWords;
	private static final String ALPHABET = "abcdefghijklmnopqrstuvwxyz";
	public SpellChecker(Map<String, Integer> words) {
		if (words == null)
			mWords = new HashMap<String, Integer>();
		else
			mWords = words;
	}

		
	public static Set<String> edits1(String word) {
		Set<String> edits = new HashSet<String>();
		List<SplitWord> splits = SplitWord.allSplits(word);
		for (SplitWord split: splits) {
			String a = split.prefix;
			String b = split.suffix;
			int lb = b.length();
			if (lb > 0) {
				edits.add(a + b.substring(1)); // delete
				for (int i = 0; i < ALPHABET.length(); ++i)
					edits.add(a + ALPHABET.charAt(i) + b.substring(1)); // replace
			}
			if (lb > 1)
				edits.add(a + b.charAt(1) + b.charAt(0) + b.substring(2)); // transpose
			for (int i = 0; i < ALPHABET.length(); ++i)
				edits.add(a + ALPHABET.charAt(i) + b); // insert
		}
		return edits;
	}
	public static Set<String> edits2(String word){//Double Edits according to norvig's spell corrector. Recursive way.
		Set<String> editsn = new HashSet<String>();
		Set<String> edits2 = new HashSet<String>();
		
		editsn.addAll(edits1(word));
		for(String w: editsn){
				edits2.addAll(edits1(w));
		}
		edits2.removeAll(editsn);
		return edits2;
	}
	// We only check for single edits and return empty of none of the possibilities are in the dictionary
	List<String> check(String word) {
		List<String> alternatives = new ArrayList<String>();
		word = word.toLowerCase();
		
		if (mWords.containsKey(word)) {
			alternatives.add(word);
			Collections.sort(alternatives);
			return alternatives;
		}
		
		Set<String> edits = edits1(word);
		for (String w: edits)
			if (mWords.containsKey(w))
				alternatives.add(w);
		Collections.sort(alternatives);
		return alternatives;
	}
	List<String> check2(String word) {
		List<String> alternatives = new ArrayList<String>();
		word = word.toLowerCase();
		
		if (mWords.containsKey(word)) {
			alternatives.add(word);
			Collections.sort(alternatives);
			return alternatives;
		}
		
		Set<String> edits = edits2(word);
		for (String w: edits)
			if (mWords.containsKey(w))
				alternatives.add(w);
		Collections.sort(alternatives);
		return alternatives;
	}
	
	
}
