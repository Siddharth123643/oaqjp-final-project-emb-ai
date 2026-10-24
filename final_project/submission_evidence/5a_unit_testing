"""Unit tests for the emotion_detector function."""
import unittest
from unittest.mock import patch, Mock
from EmotionDetection.emotion_detection import emotion_detector


class TestEmotionDetector(unittest.TestCase):
    """Tests for dominant emotion detection against live service."""

    def test_joy(self):
        """Test statement expecting joy."""
        result = emotion_detector("I am glad this happened")
        self.assertEqual(result['dominant_emotion'], 'joy')

    def test_anger(self):
        """Test statement expecting anger."""
        result = emotion_detector("I am really mad about this")
        self.assertEqual(result['dominant_emotion'], 'anger')

    def test_disgust(self):
        """Test statement expecting disgust."""
        result = emotion_detector("I feel disgusted just hearing about this")
        self.assertEqual(result['dominant_emotion'], 'disgust')

    def test_sadness(self):
        """Test statement expecting sadness."""
        result = emotion_detector("I am so sad about this")
        self.assertEqual(result['dominant_emotion'], 'sadness')

    def test_fear(self):
        """Test statement expecting fear."""
        result = emotion_detector("I am really afraid that this will happen")
        self.assertEqual(result['dominant_emotion'], 'fear')


class TestEmotionDetectorErrorHandling(unittest.TestCase):
    """Isolated unit tests for error handling and response structure."""

    def test_blank_input(self):
        """Test handling of blank string input."""
        result = emotion_detector("")
        expected = {
            'anger': None,
            'disgust': None,
            'fear': None,
            'joy': None,
            'sadness': None,
            'dominant_emotion': None
        }
        self.assertEqual(result, expected)

    def test_whitespace_input(self):
        """Test handling of whitespace-only input."""
        result = emotion_detector("   ")
        expected = {
            'anger': None,
            'disgust': None,
            'fear': None,
            'joy': None,
            'sadness': None,
            'dominant_emotion': None
        }
        self.assertEqual(result, expected)

    def test_dictionary_structure(self):
        """Test dictionary keys and structure."""
        expected_keys = {
            'anger', 'disgust', 'fear', 'joy', 'sadness', 'dominant_emotion'
        }
        result = emotion_detector("")
        self.assertEqual(set(result.keys()), expected_keys)

    @patch('requests.post')
    def test_status_400_error(self, mock_post):
        """Test handling when Watson API returns status 400."""
        mock_response = Mock()
        mock_response.status_code = 400
        mock_post.return_value = mock_response

        result = emotion_detector("Invalid input that causes 400")
        expected = {
            'anger': None,
            'disgust': None,
            'fear': None,
            'joy': None,
            'sadness': None,
            'dominant_emotion': None
        }
        self.assertEqual(result, expected)


if __name__ == '__main__':
    unittest.main()
